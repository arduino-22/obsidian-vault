# Веб-сайт

## Базовый enum

Мы можем узнать, что обслуживает сайт, изучив его заголовки:

```bash
$ curl -v http://cereal.htb
*   Trying 10.10.10.217:80...
* Connected to cereal.htb (10.10.10.217) port 80 (#0)
> GET / HTTP/1.1
> Host: cereal.htb
> User-Agent: curl/7.74.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 307 Temporary Redirect
< Transfer-Encoding: chunked
< Location: https://cereal.htb/
< Server: Microsoft-IIS/10.0
< X-Rate-Limit-Limit: 5m
< X-Rate-Limit-Remaining: 149
< X-Rate-Limit-Reset: 2021-06-05T18:26:04.5220616Z
< X-Powered-By: Sugar
< Date: Sat, 05 Jun 2021 18:21:04 GMT
< 
* Connection #0 to host cereal.htb left intact
```

`Sugar` — это интересное добавление в заголовок `X-Powered-By`, которого я раньше не видел. Также присутствует ограничение скорости, что следует учитывать.

## Сертификат

Сразу после посещения сайта Firefox показывает предупреждение о самозакрепленном сертификате

![[Pasted image 20210406083553.png]]

Нажатие «View Certificate» раскрывает поддомен `source.cereal.htb`

![[Pasted image 20210406083753.png]]

(это также было видно в сканировании Nmap)

Если мы хотим снова посмотреть сертификат после его приёма, просто нажмите замок в браузере и `>`, затем `More Information`. Это позволяет просмотреть сертификат:

![[Pasted image 20210605185025.png]]

## Форма входа

При посещении главного сайта мы видим простую форму входа:

![[Pasted image 20210605184135.png]]

Мы можем выполнить некоторый базовый фузинг формы:
- попробовать `admin:admin`
- попробовать простое SQL-инъекцию с именем/паролем `' OR 1=1;--`
- попробовать полиглот SQLi, чтобы узнать, не уязвима ли форма: `SLEEP(1) /*’ or SLEEP(1) or’” or SLEEP(1) or “*/","password":"SLEEP(1) /*’ or SLEEP(1) or’” or SLEEP(1) or “*/"`

Ничто из этого не дало результата. Также, похоже, нет способа регистрироваться — посещение `/register` показывает пустую страницу:

![[Pasted image 20210605184317.png]]

Давайте посмотрим на домен `source.cereal.htb`, чтобы увидеть, есть ли что-то ещё полезное.
