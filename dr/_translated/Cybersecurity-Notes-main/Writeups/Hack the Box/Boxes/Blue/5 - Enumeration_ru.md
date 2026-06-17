## Enumeration

## nmap

Я начал сканирование с `nmap`:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/blue]
└─$ nmap -v -sC -sV -oA nmap/ 10.10.10.40
Starting Nmap 7.91 ( https://nmap.org ) at 2021-05-01 11:53 BST
NSE: Loaded 153 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 11:53
Completed NSE at 11:53, 0.00s elapsed
Initiating NSE at 11:53
Completed NSE at 11:53, 0.00s elapsed
Initiating Ping Scan at 11:53
Scanning 10.10.10.40 [2 ports]
Completed Ping Scan at 11:53, 0.04s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 11:53
Completed Parallel DNS resolution of 1 host. at 11:53, 0.00s elapsed
Initiating Connect Scan at 11:53
Scanning 10.10.10.40 [1000 ports]
Discovered open port 135/tcp on 10.10.10.40
Discovered open port 445/tcp on 10.10.10.40
Discovered open port 139/tcp on 10.10.10.40
Discovered open port 49156/tcp on 10.10.10.40
Discovered open port 49154/tcp on 10.10.10.40
Discovered open port 49153/tcp on 10.10.10.40
Discovered open port 49152/tcp on 10.10.10.40
Discovered open port 49155/tcp on 10.10.10.40
Discovered open port 49157/tcp on 10.10.10.40
Completed Connect Scan at 11:53, 1.59s elapsed (1000 total ports)
Initiating Service scan at 11:53
Scanning 9 services on 10.10.10.40
Service scan Timing: About 44.44% done; ETC: 11:55 (0:01:08 remaining)
Completed Service scan at 11:54, 59.30s elapsed (9 services on 1 host)
NSE: Script scanning 10.10.10.40.
Initiating NSE at 11:54
Completed NSE at 11:54, 10.11s elapsed
Initiating NSE at 11:54
Completed NSE at 11:54, 0.01s elapsed
Initiating NSE at 11:54
Completed NSE at 11:54, 0.00s elapsed
Nmap scan report for 10.10.10.40
Host is up (0.026s latency).
Not shown: 991 closed ports
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49155/tcp open  msrpc        Microsoft Windows RPC
49156/tcp open  msrpc        Microsoft Windows RPC
49157/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: HARIS-PC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: -16m03s, deviation: 34m36s, median: 3m54s
| smb-os-discovery: 
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
|   Computer name: haris-PC
|   NetBIOS computer name: HARIS-PC\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2021-05-01T11:58:35+01:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge-response: supported
|_  message-signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but disabled
| smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: NT_STATUS_OBJECT_NAME_NOT_FOUND
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|_      https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/

Nmap done: 1 IP address (1 host up) scanned in 112.68 seconds
```

Shared folder `Users` особенно интересен, и содержит файлы `NTUSER.DAT`. Это профилные файлы Windows, и, по-видимому, возможно [извлечение информации о пароле](https://www.fuzzysecurity.com/tutorials/18.html) из них. Мы запишем это и возможно вернемся к ним позже, если закончится идея.

### Scан уязвимостей SMB

Я не проверил это при первом сканировании, но следующая команда немедленно указала бы, что устройство уязвимо к Eternal Blue.

```bash
┌──(mac㉿kali)-[~/Documents/Personal-Vault]
└─$ nmap --script vuln 10.10.10.40
Starting Nmap 7.91 ( https://nmap.org ) at 2021-05-01 19:41 BST
Nmap scan report for 10.10.10.40
Host is up (0.032s latency).
Not shown: 991 closed ports
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown
49156/tcp open  unknown
49157/tcp open  unknown

Host script results:
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: NT_STATUS_OBJECT_NAME_NOT_FOUND
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|_      https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/

Nmap done: 1 IP address (1 host up) scanned in 112.68 seconds
```

Я узнал о уязвимости другим способом, подробно в следующем разделе.

# Tags

#windows #enum #smb #oscp-prep
