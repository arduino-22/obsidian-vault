# FTP

Мой первый шаг был проверкой FTP.

Мы можем войти анонимно:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/devel/ftp]
└─$ ftp 10.10.10.5
Connected to 10.10.10.5.
220 Microsoft FTP Service
Name (10.10.10.5:mac): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password:
230 User logged in.
Remote system type is Windows_NT.
```

Если мы создадим файл локально, мы можем поместить его:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/devel]
└─$ mkdir ftp
┌──(mac㉿kali)-[~/Documents/HTB/devel]
└─$ echo "test" > test
┌──(mac㉿kali)-[~/Documents/HTB/devel]
└─$ mv test ftp/
```

В FTP-клиенте:

```
?Invalid command
ftp> put test
local: test remote: test
200 PORT command successful.
125 Data connection already open; Transfer starting.
226 Transfer complete.
6 bytes sent in 0.09 secs (0.0625 kB/s)
```

Таким образом у нас появляются произвольные права загрузки. Давайте проверим сайт, чтобы посмотреть, можно ли использовать это для эксплуатации.

*Примечание*: не нужно находиться в директории `ftp` при запуске клиента — мы можем подключиться к FTP и затем использовать `lcd ftp` также.
