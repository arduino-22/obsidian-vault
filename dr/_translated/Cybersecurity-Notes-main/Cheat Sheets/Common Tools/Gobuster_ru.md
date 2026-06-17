# Gobuster

Инструмент для абсурдного атакования веб-страниц (также известный как directory busting), имен DNS и виртуальных хостов — написан на [Go](https://golang.org/).

Репозиторий можно найти по адресу [https://github.com/OJ/gobuster](https://github.com/OJ/gobuster)

## Установка

### Kali Linux

`gobuster` не предустановлен на Kali Linux, но имеется пакет. Установите следующим способом:

```bash
$ sudo apt-get install gobuster
```

### Другие операционные системы

Если ваш менеджер пакетов не содержит `gobuster`, или вы хотите установить его из исходного кода на Kali вместо использования `apt`, следуйте инструкциям по установке [в репозитории](https://github.com/OJ/gobuster#easy-installation).

## Directory Busting

**Базовая синтаксис**

```bash
$ gobuster dir -u [URL] -w /path/to/wordlist
```

**Какой словарь использовать?**

Я предпочитаю использовать списки обнаружения [SecLists](https://github.com/danielmiessler/SecLists). Наиболее распространенный, который я использую, находится по адресу `/path/to/seclists/Discovery/Web-Content/raft-small-words.txt`. SecLists предустановлен на Kali Linux и лежат в `/usr/share/seclists`.

Вы также можете использовать более крупный словарь, например `raft-large-words.txt`, или словарь для конкретной платформы, такой как `tomcat.txt`, против известного сервера Tomcat.

Если вы не хотите устанавливать SecLists, некоторые дистрибьюторы предоставляют альтернативные словари, например `/usr/share/wordlists/dirb/common.txt`. Однако многие словари `dirb` упускают важные элементы, такие как проверка существования файла `.git`.

**Добавление расширений**

Если вы знаете, что целевой сайт использует определенную расширение файла, например `php` или `jsp`, можно указать это с помощью флага `-x`

```bash
$ gobuster dir -u example.com -w /path/to/wordlist -x php,asp
```

## VHOST Busting

Вы также можете использовать Gobuster для абсурдного атакования виртуальных хостов (также известных как поддомены). Для этого используйте режим `vhost`.

**Базовая синтаксис**

```bash
gobuster vhost -u example.com -w /path/to/wordlist
```

Это добавит поддомены в начало имени хоста, например `staging.example.com`. Хороший словарь можно найти по адресу `/usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt`.

Практический пример:
IppSec делает это на [Academy](https://youtu.be/yQl5RA6APyQ?t=306)

# Теги

#cheat-sheet #enum
