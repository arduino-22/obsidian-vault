# Энциклопедия

## Autorecon

Я начал с использования autorecon:

```bash
┌──(mac㉿kali)-[~/.config/AutoRecon]
└─$ autorecon 10.10.10.138
[*] Scanned target 10.10.10.138
[*] Running service detection nmap-full-tcp on 10.10.10.138
[*] Running service detection nmap-top-20-udp on 10.10.10.138
[*] Running service detection nmap-quick on 10.10.10.138
[!] Service detection nmap-top-20-udp on 10.10.10.138 returned non-zero exit code: 1
[*] Service detection nmap-quick on 10.10.10.138 finished successfully in 25 seconds
[*] Found ssh on tcp/22 on target 10.10.10.138
[*] Found http on tcp/80 on target 10.10.10.138
[*] Running task tcp/22/sslscan on 10.10.10.138
[*] Running task tcp/22/nmap-ssh on 10.10.10.138
[*] Running task tcp/80/sslscan on 10.10.10.138
[*] Running task tcp/80/nmap-http on 10.10.10.138
[*] Running task tcp/80/curl-index on 10.10.10.138
[*] Running task tcp/80/curl-robots on 10.10.10.138
[*] Running task tcp/80/wkhtmltoimage on 10.10.10.138
[*] Running task tcp/80/whatweb on 10.10.10.138
[*] Running task tcp/80/nikto on 10.10.10.138
[*] Task tcp/22/sslscan on 10.10.10.138 finished successfully in 1 second
[*] Running task tcp/80/gobuster on 10.10.10.138
[*] Task tcp/80/sslscan on 10.10.10.138 finished successfully in 1 second
[!] Task tcp/80/gobuster on 10.10.10.138 returned non-zero exit code: 1
[*] Task tcp/80/curl-index on 10.10.10.138 finished successfully in 4 seconds
[*] Task tcp/80/curl-robots on 10.10.10.138 finished successfully in 7 seconds
[*] Task tcp/22/nmap-ssh on 10.10.10.138 finished successfully in 14 seconds
[*] Task tcp/80/nikto on 10.10.10.138 finished successfully in 16 seconds
[*] Task tcp/80/nmap-http on 10.10.10.138 finished successfully in 16 seconds
[!] Task tcp/80/wkhtmltoimage on 10.10.10.138 returned non-zero exit code: 1
[*] [20:18:15] - There are 2 tasks still running on 10.10.10.138
[*] Task tcp/80/whatweb on 10.10.10.138 finished successfully in 36 seconds
[*] [20:19:15] - There is 1 task still running on 10.10.10.138
[*] Service detection nmap-full-tcp on 10.10.10.138 finished successfully in 2 minutes, 51 seconds
[*] Found tcpwrapped on tcp/80 on target 10.10.10.138
[*] Running task tcp/80/sslscan on 10.10.10.138
[*] Task tcp/80/sslscan on 10.10.10.138 finished successfully in less than a second
[*] Finished scanning target 10.10.10.138 in 2 minutes, 52 seconds
[*] Finished scanning all targets in 2 minutes, 52 seconds!
```

Он сразу же обнаружил вебсервер и SSH.

## nmap

Я просмотрел результаты сканирования от autorecon:

```bash
┌──(mac㉿kali)-[~/Документы/HTB/писмо/резулеты/10.10.10.138/сканиры]
└─$ cat _full_tcp_nmap.txt 
# Nmap 7.91 scan initiated Thu Jul 15 20:17:16 2021 as: nmap -vv --reason -Pn -A --osscan-guess --version-all -p- -oN /home/mac/.config/AutoRecon/резулеты/10.10.10.138/сканиры/_full_tcp_nmap.txt -oX /home/mac/.config/AutoRecon/резулеты/10.10.10.138/сканиры/xml/_full_tcp_nmap.xml 10.10.10.138
Nmap scan report for 10.10.10.138
Host is up, received user-set (0.016s latency).
Scanned at 2021-07-15 20:17:19 BST for 164s
Not shown: 65533 filtered ports
Reason: 65533 no-responses
PORT   STATE SERVICE    REASON  VERSION
22/tcp open  ssh        syn-ack OpenSSH 7.4p1 Debian 10+deb9u6 (protocol 2.0)
| ssh-hostkey: 
|   2048 dd:53:10:70:0b:d0:47:0a:e2:7e:4a:b6:42:98:23:c7 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDKBbBK0GkiCbxmAbaYsF4DjDQ3JqErzEazl3v8OndVhynlxNA5sMnQmyH+7ZPdDx9IxvWFWkdvPDJC0rUj1CzOTOEjN61Qd7uQbo5x4rJd3PAgqU21H9NyuXt+T1S/Ud77xKei7fXt5kk1aL0/mqj8wTk6HDp0ZWrGBPCxcOxfE7NBcY3W++IIArn6irQUom0/AAtR3BseOf/ VTdDWOXk/Ut3rrda4VMBpRcmTthjsTXAvKvPJcaWJATtRE2NmFjBWix
```

Возможно, проблема не в autorecon — соединение отклонено, но я могу получить доступ к [[Писмо/Хак Бокс/Комплета/10 - Сайт|сайту]], поэтому, возможно, nmap отклоняет пакеты из-за user agent.

Я попробовал снова позже, после того как узнал о Web Application Firewall на компьютере:

```bash
┌──(mac㉿kali)-[~/Документы/HTB/писмо]
└─$ nmap -p 80 -sC -sV 10.10.10.138
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-15 20:47 BST
Nmap scan report for writeup.htb (10.10.10.138)
Host is up (0.060s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.25 ((Debian))
| http-robots.txt: 1 disallowed entry 
|_/writeup/
|_http-title: Nothing here yet.

Service detection performed. Please report any incorrect results at https://nmap.org/submit/.
Nmap done: 1 IP address (1 host up) scanned in 13.60 seconds
```

Это выявил `robots.txt` и директорию writeup, что уже было известно мне ранее.
