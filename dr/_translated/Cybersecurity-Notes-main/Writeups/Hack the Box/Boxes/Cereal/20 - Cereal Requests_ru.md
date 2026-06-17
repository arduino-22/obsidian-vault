# Запросы на cereal

Тепер, когда мы немного разобрали код, можем попробовать взаимодействовать с сайтом.

Если перейти на `/requests` в браузере и передать запрос через Burp, мы сможем захватить запрос, а затем изменить метод запроса:

![[Pasted image 20210406085414.png]]

Мы можем нажать `Ctrl + R`, чтобы отправить запрос в репитера, затем щелкнуть правой кнопкой и выбрать «Change request method», чтобы превратить его в POST-запрос. Нам также нужно установить заголовок `Content-Type` на `application/json`, так как приложение ожидает JSON, а в противном случае откликается с `415 Unsupported Media Type`.

![[Pasted image 20210406085814.png]]

Давайте добавим наш токен в запрос. Мы добавляем следующий заголовок: `Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MTgzMDA5ODMsIm5hbWUiOjF9.VgWvwKp0RMrr4NLnJxnIWoUJII3JQlUJecyFVpDlXvo` и повторно отправляем запрос.

*Примечание:* Это просто токен, который я использовал при выполнении этого задания — он истечет через семь дней, поэтому если вы выполняете это задание, вам нужно создать свой токен с помощью `gentoken.py`.

![[Pasted image 20210406090351.png]]

Теперь мы больше не без разрешения :)

Теперь нам нужно создать корректный запрос. Эксперименты с вводом JSON дают нам подсказки о структуре запроса — а именно, что поле `"JSON"` обязательно:

![[Pasted image 20210406090615.png]]

Подачу еще большего JSON показывает больше информации о том, как она должна быть структурирована:

![[Pasted image 20210406091211.png]]

Похоже, необходимы символы `"` для экранирования — в исходном коде были некоторые подсказки на этот счет, например `var header = "{\\"typ\\":\\"JWT\\",\\"alg\\":\\"HS256\\"}";`, но чтобы быть уверенными, я форматировал payload, проходя его через метод `JSON.stringify()`, который использует сайт.

Я создал файл JS `test-www/stringify.js`:

```javascript
console.log(JSON.stringify({ JSON: JSON.stringify({title:'t',flavor:'f',color:'#FFF',description:'d' }) }))
```

И запустил его из очень простого файла HTML:

```html
<html>
    <head>
        <script defer src="./stringify.js"></script>
    </head>
</html>
```

Затем открыл его в Firefox:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/cereal/test-www]
└─$ firefox index.html
```

![[Pasted image 20210406092035.png]]

Это дает нам правильно форматированный payload:

```
{"JSON":"{\"title\":\"t\",\"flavor\":\"f\",\"color\":\"#FFF\",\"description\":\"d\"}"}
```

![[Pasted image 20210406092416.png]]

Мы успешно создали cereal!

Я попытался сохранить запрос Burp как команду `curl`, но он был довольно нестабильным. Чтобы имитировать запрос в `curl`, щелкните правой кнопкой в репитере и нажмите «Copy as curl command». Мне легче делать это в Burp Suite в первый раз, так как он автоматически создает многие заголовки, но для последующего имитации `curl` быстрее:

```bash
curl -i -s -k -X $'POST' \
    -H $'Host: 10.10.10.217' -H $'User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0' -H $'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8' -H $'Accept-Language: en-US,en;q=0.5' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' -H $'Upgrade-Insecure-Requests: 1' -H $'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MTgzMDA5ODMsIm5hbWUiOjF9.VgWvwKp0RMrr4NLnJxnIWoUJII3JQlUJecyFVpDlXvo' -H $'Content-Type: application/json' -H $'Content-Length: 86' \
    --data-binary $'{\"JSON\":\"{\\\"title\\\":\\\"t\\\",\\\"flavor\\\":\\\"f\\\",\\\"color\\\":\\\"#FFF\\\",\\\"description\\\":\\\"d\\\"}\"}' \
    $'https://10.10.10.217/requests'
```
