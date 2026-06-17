# Перечисление

## nmap

Я начал сканирование с `nmap`, чтобы выявить открытые порты:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/bucket]
└─$ nmap 10.10.10.212 -sC -sV -oA nmap/  
Начинается Nmap 7.80 (https://nmap.org) в 2020-12-15 15:04 GMT  
Отчет сканирования Nmap для 10.10.10.212  
Хост работает (задержка 0.032 с).  
Не показано: 998 закрытых портов  
Порт Статус Сервис Версия  
22/tcp open ssh OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)  
80/tcp open http Apache httpd 2.4.41  
|_http-server-header: Apache/2.4.41 (Ubuntu)  
|_http-title: Did not follow redirect to http://bucket.htb/  
Информация о сервисе: Хост: 127.0.1.1; ОС: Linux; CPE: cpe:/o:linux:linux\kernel  
  
Отчет об обнаружении сервиса выполнен. Пожалуйста, сообщите любые неверные результаты по адресу https://nmap.org/submit/.  
Конец Nmap: 1 IP-адрес (1 хост работает) сканирован за 8.45 секунд
```

Это показывает, что только порты 22 и 80 открыты, для SSH и HTTP. Это означает, что мы должны начать с рассмотрения [[Writeups/Hack the Box/Boxes/Bucket/10 - Website|website]]

## Gobuster

Я запустил gobuster на домене веб-сайта:

```bash
┌──(mac㉿kali)-[~/Documents/enum]
└─$ gobuster dir -u http://10.10.10.212 -w /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.10.212
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/04/28 12:31:01 Начинается gobuster в режиме эскалации каталогов
===============================================================
Ошибка: сервер возвращает статус-код, соответствующий предоставленным параметрам для несуществующих URL. http://10.10.10.212/84530f45-4eb0-4f43-bae7-e0227949c00c => 302 (Длина: 280). Чтобы продолжить, пожалуйста, исключите статус-код, длину или используйте параметр --wildcard
```

Запуск с параметром `--wildcard` возвращает большое количество статус-кодов `302`.

Когда я обнаружил домен `bucket.htb`, я повторно запустил сканирование:

```bash
┌──(mac㉿kali)-[~/Documents/enum]
└─$ gobuster dir -u http://bucket.htb --wildcard -w /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://bucket.htb
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/04/28 12:33:51 Начинается gobuster в режиме эскалации каталогов
===============================================================
/.php                 (Status: 403) [Size: 275]
/.html                (Status: 403) [Size: 275]
/.htm                 (Status: 403) [Size: 275]
/.                    (Status: 200) [Size: 5344]
/.htaccess            (Status: 403) [Size: 275] 
/.phtml               (Status: 403) [Size: 275] 
/.htc                 (Status: 403) [Size: 275] 
/.html_var_DE         (Status: 403) [Size: 275] 
/server-status        (Status: 403) [Size: 275] 
/.htpasswd            (Status: 403) [Size: 275] 
/.html.               (Status: 403) [Size: 275] 
/.html.html           (Status: 403) [Size: 275] 
/.htpasswds           (Status: 403) [Size: 275] 
/.htm.                (Status: 403) [Size: 275] 
/.htmll               (Status: 403) [Size: 275] 
/.phps                (Status: 403) [Size: 275] 
/.html.old            (Status: 403) [Size: 275] 
/.ht                  (Status: 403) [Size: 275] 
/.html.bak            (Status: 403) [Size: 275] 
/.htm.htm             (Status: 403) [Size: 275] 
/.hta                 (Status: 403) [Size: 275] 
/.html1               (Status: 403) [Size: 275] 
/.htgroup             (Status: 403) [Size: 275] 
/.html.LCK            (Status: 403) [Size: 275] 
/.html.printable      (Status: 403) [Size: 275] 
/.htm.LCK             (Status: 403) [Size: 275] 
/.htaccess.bak        (Status: 403) [Size: 275] 
/.html.php            (Status: 403) [Size: 275] 
/.htmls               (Status: 403) [Size: 275] 
/.htx                 (Status: 403) [Size: 275] 
/.htlm                (Status: 403) [Size: 275] 
/.htm2                (Status: 403) [Size: 275] 
/.html-               (Status: 403) [Size: 275] 
/.htuser              (Status: 403) [Size: 275] 
                                                
===============================================================
2021/04/28 12:35:26 Завершено
===============================================================
```

Здесь не было полезных результатов.

### s3.bucket.htb

После обнаружения поддомена `s3`, я запустил gobuster против него:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/bucket]
└─$ gobuster dir -u s3.bucket.htb -w /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://s3.bucket.htb
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/04/29 13:52:34 Начинается gobuster в режиме эскалации каталогов
===============================================================
/health               (Status: 200) [Size: 54]
/shell                (Status: 200) [Size: 0] 
/server-status        (Status: 403) [Size: 278]
/shells               (Status: 500) [Size: 158]
                                               
===============================================================
2021/04/29 14:00:08 Завершено
===============================================================
```

Это раскрыло страницы `/health` и `shell`.

# Теги

#writeup
