---
icon: 🔑
target:
  - "[[exemplo.com.br]]"
---
## Сертификаты
```
Peter:Peter@1234
```

# Чек-лист  
- [ ] Проверить все сертификаты на всех хостах  
  - [ ] WMI  
  - [ ] RDP  
  - [ ] WinRM  
  - [ ] PsExec  
- [ ] Проверить сертификаты локально (`nxc` / `--local-auth`)  

### NTLM Hash  
- [ ] Выполнить Pass The Hash на всех хостах  
- [ ] Попытка взлома с использованием Hashcat  

### Plaintext  
- [ ] Проверить пароль на всех других идентифицированных сертификатах (password spray)  

## Советы  
Вы можете проверить все сертификаты в networkx
```
nxc smb 192.168.1.0/24 -u web_svc -p 'senha'
nxc wmi 192.168.1.0/24 -u web_svc -p 'senha'
nxc winrm 192.168.1.0/24 -u web_svc -p 'senha'
nxc rdp 192.168.1.0/24 -u web_svc -p 'senha' 
```

```
nxc smb 192.168.1.0/24 -u web_svc -p '' --local 
```
## Связанная записка  
NotaRelacionada
```
