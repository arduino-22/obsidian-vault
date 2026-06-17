# Website

Посетив `http://10.10.10.226:5000` мы видим сайт, полный «инструментов хакера»:

![[Pasted image 20210612124335.png]]

Похоже, под капотом будет выполняться некоторые распространённые команды линукс для pen-тестов. Давайте попробуем несколько.

## Nmap

Давайте попробуем нанмаппинг самого компьютера, отправив `127.0.0.1`:

![[Pasted image 20210612124713.png]]

Круто! Это работает, и может быть полезно, если позже обнаружится какой-то недостаток SSRF. А что, если будет форма командной инジェкции?

Я попробовал несколько пайлотов здесь:
- `127.0.0.1 && id`
- `127.0.0.1; id`
- `127.0.0.1 -oA local` (чтобы увидеть, не блокирует ли он традиционные синтаксисы командной инジェкции, но принимает другие команды)

Все они дали одну и ту же ответ: «invalid ip»:

![[Pasted image 20210612124906.png]]

Ничего страшного — давайте перейдём к следующей команде.

## Пайлоты

Это «генератор пайлотов», что заставляет меня подумать, что, возможно, выполняется что-то вроде `msfvenom`.

### Попытка загрузки шаблона обратного шелла

Есть опция выбора операционной системы и опция загрузки файла шаблона. Может быть, мы можем загрузить обратный шелл на компьютер через загрузку шаблона?

Просмотр сайта в режиме verbose не сообщает нам ничего нового о том, что он выполняет:

```bash
┌──(mac㉿kali)-[~]
└─$ curl -v 10.10.10.226:5000
*   Trying 10.10.10.226:5000...
* Connected to 10.10.10.226 (10.10.10.226) port 5000 (#0)
> GET / HTTP/1.1
> Host: 10.10.10.226:5000
> User-Agent: curl/7.74.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
* HTTP 1.0, assume close after body
< HTTP/1.0 200 OK
< Content-Type: text/html; charset=utf-8
< Content-Length: 2135
< Server: Werkzeug/0.16.1 Python/3.8.5
< Date: Sat, 12 Jun 2021 12:00:52 GMT
```

Я не уверен, какой формат использовать для пайлота на сервере Werkzeug — из опыта с flask я доволен, что он не просто выполнит файл, если посетим его путь. Мы также не обнаружили какой-либо путь `/uploads` в нашем сканировании [[Writeups/Hack the Box/Boxes/Scriptkiddie/5 - Enumeration#Gobuster|Gobuster]], но давайте просто сгенерируем общий пайлот и посмотрим, что произойдёт:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/scriptkiddie]
└─$ msfvenom -p linux/x64/shell_reverse_tcp -o test_shell
[-] No platform was selected, choosing Msf::Module::Platform::Linux from the payload
[-] No arch selected, selecting arch: x64 from the payload
No encoder specified, outputting raw payload
Payload size: 74 bytes
Saved as: test_shell
```

Нам не особо важны настройки пайлота, который генерирует *сайт* — мы просто хотим сохранить нашу зловредную шаблоку:

![[Pasted image 20210612125842.png]]

Однако это не работает:

![[Pasted image 20210612125902.png]]

Windows требует exe. Так что, если мы выберем linux как ОС, будет ли он принимать наш файл? На этот раз требуется ELF:

![[Pasted image 20210612130005.png]]

В первый раз, когда я делал это, я искал файл ELF и взял его magic bytes, затем отправил его в тестовый файл, просто чтобы увидеть, будет ли он загрузить:

```bash
$ head -c 8 ~/Documents/enum/pspy64 > elfy
$ file elfy
elfy: ELF 64-bit LSB (SYSV)
$ echo "hello" >> elfy
$ file elfy
elfy: ELF 64-bit LSB (SYSV)
```

Однако можно также генерировать ELF с msfvenom, что я попробовал во второй раз:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/scriptkiddie]
└─$ msfvenom -p linux/x64/shell_reverse_tcp -f elf -o test_elf
[-] No platform was selected, choosing Msf::Module::Platform::Linux from the payload
[-] No arch selected, selecting arch: x64 from the payload
No encoder specified, outputting raw payload
Payload size: 74 bytes
Final size of elf file: 194 bytes
Saved as: test_elf
```

Я отправил это:

![[Pasted image 20210612130520.png]]

Но получил тот же ошибку. Так что я попробовал снова с расширением `.elf`:

![[Pasted image 20210612130731.png]]

На этот раз сервер застрял на некоторое время, и в конце концов вывел «что-то пошло не так»:

![[Pasted image 20210612130829.png]]

Это указывает на то, что на самом деле под капотом выполняется что-то вроде `msfvenom`, потому что всегда требуется некоторое время для выполнения.

Я подумал искать файл на системе — по gobuster не было директории `/uploads/`, но что, если он сохранён в `/payloads/`? Или просто в `/test_elf.elf`?

Оба этих пути дали 404:

![[Pasted image 20210612131021.png]]

Давайте попробуем создать работающий пайлот и посмотрим, может ли он сообщить нам путь файла. Сначала включим Burp Suite, затем попробуем базовый Android пайлот без файла шаблона, чтобы увидеть, что произойдёт. Вот запрос в Burp:

![[Pasted image 20210612131404.png]]

В этом запросе может быть несколько параметров для фузинга. Но пока давайте посмотрим, что произойдёт. Это работает!

![[Pasted image 20210612131340.png]]

Страница выводит ссылку на `/static/payloads/[HASH]` для загрузки пайлота:

![[Pasted image 20210612131505.png]]

Я попробовал искать наши зловредные шаблоки в этой директории и в `/static/templates/`, но ничего не вышло:

![[Pasted image 20210612131600.png]] (предположительно, изображение не загружено)

---
