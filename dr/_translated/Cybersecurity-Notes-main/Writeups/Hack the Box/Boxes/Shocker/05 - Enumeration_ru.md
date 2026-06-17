# Enumeration

## Nmap

Я начал сканирование с помощью `nmap`:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/shocker]
└─$ nmap -sC -sV -v -Pn -oA nmap/shocker 10.10.10.56
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-14 08:22 BST
NSE: Loaded 153 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 08:22
Completed Parallel DNS resolution of 1 host. at 08:22, 0.00s elapsed
Initiating Connect Scan at 08:22
Scanning 10.10.10.56 [1000 ports]
Discovered open port 80/tcp on 10.10.10.56
Discovered open port 2222/tcp on 10.10.10.56
Completed Connect Scan at 08:22, 0.46s elapsed (1000 total ports)
Initiating Service scan at 08:22
Scanning 2 services on 10.10.10.56
Completed Service scan at 08:22, 6.12s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.10.56.
Initiating NSE at 08:22
Completed NSE at 08:22, 1.53s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating NSE at 08:22
Completed N
