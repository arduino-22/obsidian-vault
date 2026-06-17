# Enumeration

## nmap

Я начал с `nmap`, используя флаг `-v`, чтобы увидеть порты, которые обнаружены.

```bash
┌──(mac㉿kali)-[~/Documents/HTB/granny]
└─$ nmap -sC -sV -v -oA nmap/ 10.10.10.15
Starting Nmap 7.91 ( https://nmap.org ) at 2021-05-06 08:29 BST
NSE: Loaded 153 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 08:29
Completed NSE at 08:29, 0.00s elapsed
Initiating NSE at 08:29
Completed NSE at 08:29, 0.00s elapsed
Initiating NSE at 08:29
Completed NSE at 08:29, 0.00s elapsed
Initiating Ping Scan at 08:29
Scanning 10.10.10.15 [2 ports]
Completed Ping Scan at 08:29, 0.04s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 08:29
Completed Parallel DNS resolution of 1 host. at 08:29, 0.00s elapsed
Initiating Connect Scan at 08:29
Scanning 10.10.10.15 [1000 ports]
Discovered open port 80/tcp on 10.10.10.15
Completed Connect Scan at 08:29, 8.61s elapsed (1000 total ports)
Initiating Service scan at 08:29
Scanning 1 service on 10.10.10.15
Completed Service scan at 08:29, 6.14s elapsed (1 service on 1 host)
NSE: Script scanning 10.10.10.15.
Initiating NSE at 08:29
Completed NSE at 08:29, 0.59s elapsed
Initiating NSE at 08:29
Completed NSE at 08:29, 0.09s elapsed
Initiating NSE at 08:29
Completed NSE at 08:29, 0.00s elapsed
Nmap scan report for 10.10.10.15
Host is up (0.030s latency).
Not shown: 999 filtered ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD DELETE COPY MOVE PROPFIND PROPPATCH SEARCH MKCOL LOCK UNLOCK PUT
|_  Potentially risky methods: TRACE DELETE COPY MOVE PROPFIND PROPPATCH SEARCH MKCOL LOCK UNLOCK PUT
|_http-server-header: Microsoft-IIS/6.0
|_http-title: Under Construction
| http-webdav-scan: 
|_Negative Status codes:   404
| Wordlist:                /usr/share/seclists/Discovery/Web-Content/raft-small-directories.txt
===============================================================
```

---

# Enumeration

## nmap
