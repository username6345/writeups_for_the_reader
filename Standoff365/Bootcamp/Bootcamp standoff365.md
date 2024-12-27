#### Дисклеймер 
Дисклеймер- Данная часть архива расчитана на то что вы смотрите его через приложение Obsidian. Данный архив содержит решения и заметки по различным темам. Если у вас возникнут вопросы, не стесняйтесь обращаться на почту from64 dmFzeWEua290b3YuODA4MEBtYWlsLnJ1 (чтобы боты не парсили )  . Автор этого архива регулярно делится своими заметками и writeups. Обратите внимание, что формат написания будет совершенствоваться с течением времени.

Обратите внимание, что в архиве могут содержаться черновики и незавершенные задания. Читателям рекомендуется учитывать этот факт.

---

#### Мини подсказки для работы с obsidian 
Ctr+e  Перейти в формат чтения/редактирования
Ctr+g  Открыть graph/граф 
Ctr+Click (левая кнопка мыши) Открыть ссылку в соседнем окне

Слева и справа в интерфейсе обсидиана вы можете найти:
Слева-> Файловый менеджер: со списком файлов и их расположением папко
Справа-> Оглавление
![](image/Pasted%20image%2020241226110340.png)

Все Фотографии/Скрины Вы можете найти в подпапке image и все производные папки со сходими названиями .В случае если нужно найти какое то конкретно изображение вы можетей открыть его в новом окне , для этого переходим в режим редактирования , переходим к строке чуть выше изображение и увидим что то вроде : 
Пример ниже:
---!Скрин а не текст---

![](image/Pasted%20image%2020241226110614.png)---!Скрин а не текст Конец---
Открыв его в новом окне нажием на 3 точке справа , и ищем  "Показать в папке"

Для более быстрого перемещения можно использовать файловый менеджер или 
Ctr+o Перейти к названию файла

![](image/Obsidian_LWjDhl2QDD.mp4)

---
#### Сылки на задания 

![[детский полигон.canvas]]


Файл содержимащий мини отчёты по сканироваю различных инструмнетов:
[[infra/internal network|internal network]]

✅[[web-1-1  web-1-2 library.edu.stf]] =  [web1-1_1-2](https://codeby.net/threads/writeup-web-1-1-web-1-2-library-edu-stf-standoff-365.84062/)    |     [en_web-1-3](https://medium.com/@alex122303q/my-standoff365-ctf-web-1-x-assignment-adventure-how-i-hacked-a-website-legally-of-course-a8bff200dbc3 )  

❌[[web-2-1 www.edu.stf]]
[[web-2-2]]
[web-2-3](web/web-2-3.md)

✅[[web-3-1 utils.edu.stf]]
✅[[web-3-2]]  [Статья кодебай](https://codeby.net/threads/writeup-web-3-1-web-3-2-utils-edu-stf-standoff365.84031/#post-437585) 

✅[[web-4]]  [статья кодебай ](https://codeby.net/threads/te-samye-fotki-s-servera-18-standoff-ctf-web-4-udalennoe-vypolnenie-koda-rce-na-uzle-shop-edu-stf.83985/)
✅[[web-5 tokenizer.edu.stf]] [стать кодебай](https://codeby.net/threads/writeup-web-5-tokenizer-edu-stf-standoff365.83968/)    |   [[web-5-en]]  [medium](https://readmedium.com/@alex122303q/scandals-intrigues-investigations-how-jwt-and-sql-caused-a-stir-in-my-session-959b0e9fa414) 
 
✅[[web-6 smashmusic.edu.stf 10.124.1.241]]
✅[[web-7]]
❌[[web-8]]
[[web-9 10.124.1.234]]
✅[[web-10]]

---

✅[[infra-1]] [codeby+](https://codeby.net/threads/writeup-standoff365-infra-1-2-3.83966/)
✅[[infra-2]] codeby+
✅[[infra-3]] codeby+
✅[[infra-4]]
[[infra-5]]
[[infra-6]]
[infra-7](infra/infra-7.md)
✅[[infra-8]] 
[[infra-9]]
[[infra-10]]
 [[infra-11]]
✅ [[infra-12]]


[[10.124.1.231 aircraft.edu.stf]]
[[10.124.1.232]]
[[10.124.1.233]]
[[10.124.1.234 wp.edu.stf]]
[[10.124.1.240 bind.edu.stf]]
[[10.124.1.253 vpn.edu.stf]]

 [[1Утечка персональных данных сотрудников]]
 [[2Сбой в работе вычислительной системы|2Сбой в работе вычислительной системы]]
 [[3Утечка конфиденциальной информации|3Утечка конфиденциальной информации]]
 [[4Получение доступа к учетной записи администратора серверов|4Получение доступа к учетной записи администратора серверов]]
 [[5Сбой в системе регистрации пассажиров|5Сбой в системе регистрации пассажиров]]

 

### Райтапы не отосящиеся к авторству: Archive

#### Web-5 Видео решение

Авторство- скрин ниже 
Публикация-  сообщение https://t.me/standoff_365_chat/94799 чат- https://t.me/standoff_365_chat 
(его нет , но мб потом будет Название видео- Tg-web5-rrradio.mp4)

![](image/Pasted%20image%2020241226104323.png)



 

---


### Черновики 

вот такая фраза
```
В ходе решения и поиска истины были выписаны большая часть не нужных сведений, но  вдруг они  потом пригодятся
```


 
#### nmap network
```
nmap -sP 10.124.1.224/27

Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-25 12:49 EDT
Nmap scan report for aircraft.edu.stf (10.124.1.231)
Host is up (0.0053s latency).
Nmap scan report for calculator.edu.stf (10.124.1.232)
Host is up (0.0053s latency).
Nmap scan report for library.edu.stf (10.124.1.233)
Host is up (0.0058s latency).
Nmap scan report for wp.edu.stf (10.124.1.234)
Host is up (0.0057s latency).
Nmap scan report for www.edu.stf (10.124.1.235)
Host is up (0.0047s latency).
Nmap scan report for gallery.edu.stf (10.124.1.236)
Host is up (0.0045s latency).
Nmap scan report for utils.edu.stf (10.124.1.237)
Host is up (0.0039s latency).
Nmap scan report for shop.edu.stf (10.124.1.238)
Host is up (0.0044s latency).
Nmap scan report for tokenizer.edu.stf (10.124.1.239)
Host is up (0.0043s latency).
Nmap scan report for bind.edu.stf (10.124.1.240)
Host is up (0.0042s latency).
Nmap scan report for smashmusic.edu.stf (10.124.1.241)
Host is up (0.0046s latency).
Nmap scan report for test-webserver.edu.stf (10.124.1.242)
Host is up (0.0048s latency).
Nmap scan report for vpn.edu.stf (10.124.1.253)
Host is up (0.0039s latency).
Nmap done: 32 IP addresses (13 hosts up) scanned in 1.31 seconds

```
#### etc/hosts 
Записано не все  хосты\ip
```
10.124.1.231    aircraft.edu.stf
10.124.1.232    calculator.edu.stf
10.124.1.233    library.edu.stf
10.124.1.234    wp.edu.stf
10.124.1.235    www.edu.stf
10.124.1.236    gallery.edu.stf
10.124.1.237    utils.edu.stf
10.124.1.238    shop.edu.stf
10.124.1.239    tokenizer.edu.stf
10.124.1.240    bind.edu.stf
10.124.1.241    smashmusic.edu.stf
10.124.1.242    test-webserver.edu.stf
10.124.1.253    vpn.edu.stf

web-1 library.edu.stf
w2 www.edu.stf 
w3 utils.edu.stf
w4 shop.edu.stf
w5  tokenizer.edu.stf
w6 smashmusic.edu.stf
w7 test-webserver.edu.stf
w8 gallery.edu.stf
w9 =w2 = wp.edu.stf
w10  calculator.edu.stf

 
10.124.1.231    aircraft.edu.stf
10.124.1.240    bind.edu.stf
10.124.1.253    vpn.edu.stf
```



