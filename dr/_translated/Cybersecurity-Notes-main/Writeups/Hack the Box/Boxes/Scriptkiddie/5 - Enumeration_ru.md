# Перечисление

## Автодетекция

Сначала я выполнил автодетекцию по клиенту:

```bash
autorecon 10.10.10.226
[*] Scanning target 10.10.10.226
[*] Running service detection nmap-top-20-udp on 10.10.10.226
[*] Running service detection nmap-full-tcp on 10.10.10.226
[*] Running service detection nmap-quick on 10.10.10.226
[*] Service detection nmap-quick on 10.10.10.226 finished successfully in 29 seconds
[*] Found ssh on tcp/22 on target 10.10.10.226
[*] Found http on tcp/5000 on target 10.10.10.226
[*] Running task tcp/22/sslscan on 10.10.10.226
[*] Running task tcp/22/nmap-ssh on 10.10.10.226
[*] Running task tcp/5000/sslscan on 10.10.10.226
[*] Running task tcp/5000/nmap-http on 10.10.10.226
[*] Running task tcp/5000/curl-robots on 10.10.10.226
[*] Running task tcp/5000/wkhtmltoimage on 10.10.10.226
[*] Running task tcp/5000/whatweb on 10.10.10.226
[*] Task tcp/22/sslscan on 10.10.10.226 finished successfully in less than a second
[*] Task tcp/5000/sslscan on 10.10.10.226 finished successfully in less than a second
[*] Running task tcp/5000/nikto on 10.10.10.226
[*] Running task tcp/5000/gobuster on 10.10.10.226
[*] Task tcp/5000/curl-robots on 10.10.10.226 finished successfully in less than a second
[*] Task tcp/5000/curl-index on 10.10.10.226 finished successfully in less than a second
[*] Task tcp/22/nmap-ssh on 10.10.10.226 finished successfully in 7 seconds
[*] Task tcp/5000/wkhtmltoimage on 10.10.10.226 finished successfully in 11 seconds
[*] Task tcp/5000/whatweb on 10.10.10.226 finished successfully in 16 seconds
[*] [10:53:56] - There are 5 tasks still running on 10.10.10.226
[*] Service detection nmap-top-20-udp on 10.10.10.226 finished successfully in 1 minute, 43 seconds
[*] [10:54:56] - There are 4 tasks still running on 10.10.10.226
[*] [10:55:56] - There are 4 tasks still running on 10.10.10.226
[*] [10:56:56] - There are 4 tasks still running on 10.10.10.226
[*] [10:57:56] - There are 4 tasks still running on 10.10.10.226
[*] [10:58:56] - There are 4 tasks still running on 10.10.10.226
[*] [10:59:56] - There are 4 tasks still running on 10.10.10.226
[*] [11:00:56] - There are 4 tasks still running on 10.10.10.226
[*] [11:01:56] - There are 4 tasks still running on 10.10.10.226
[*] [11:02:56] - There are 4 tasks still running on 10.10.10.226
[*] [11:03:56] - There are 4 tasks still running on 10.10.10.226
[*] [11:04:56] - There are 4 tasks still running on 10.10.10.226
[*] [11:05:56] - There are 4 tasks still running on 10.10.10.226
[*] [11:06:56] - There are 4 tasks still running on 10.10.10.226
[*] [11:07:56] - There are 4 tasks still running on 10.10.10.226
[*] Task tcp/5000/nmap-http on 10.10.10.226 finished successfully in 14 minutes, 57 seconds
[*] [11:08:56] - There are 3 tasks still running on 10.10.10.226
[*] Task tcp/5000/nikto on 10.10.10.226 finished successfully in 16 minutes, 7 seconds
[*] [11:09:56] - There are 2 tasks still running on 10.10.10.226
[*] [11:10:56] - There are 2 tasks still running on 10.10.10.226
[*] [11:11:56] - There are 2 tasks still running on 10.10.10.226
[*] [11:12:56] - There are 2 tasks still running on 10.10.10.226
[*] Task tcp/5000/gobuster on 10.10.10.226 finished successfully in 19 minutes, 45 seconds
[*] [11:13:56] - There is 1 task still running on 10.10.10.226
...[snip]...
| http-methods: 
|_  Supported Methods: POST GET HEAD OPTIONS
|_http-server-header: Werkzeug/0.16.1 Python/3.8.5
|_http-title: k1d'5 h4ck3r t00l5
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Feb 13 10:53:25 2021 -- 1 IP address (1 host up) scanned in 28.98 seconds
```

Ключевые выводы:
- SSH на порту 22
- Сервер работает под Ubuntu согласно строке OpenSSL
- Werkzeug вебсервер работает на порту 5000. Проверка версии через searchesploit не выявила ничего интересного

## Gobuster

Я выполнил быструю проверку по Gobuster:

```bash
┌──(mac㉿kali)-[~]
└─$ gobuster dir -u http://10.10.10.226:5000 -w /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.10.226:5000
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/06/12 12:46:02 Starting gobuster in directory enumeration mode
===============================================================
```

Ничего не найдено.
