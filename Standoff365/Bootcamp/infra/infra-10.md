Задание:

Получите доступ к компьютеру пользователя из группы администраторов рабочих станций (lshepherd.edu.stf) и к содержимому файла flag.txt.
Подсказки не отображаются при отключенном VPN. Чтобы их просмотреть, настройте VPN-подключение.



---
#### DNS + nmap 
узнали айпи
```
nslookup  lshepherd.edu.stf  10.154.16.134                      
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   lshepherd.edu.stf
Address: 10.154.17.228

```


фул скан 
```
nmap -sV -Pn -p- -T5 -A 10.154.17.228   
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-20 08:52 EST
Nmap scan report for 10.154.17.228
Host is up (0.011s latency).
Not shown: 49138 filtered tcp ports (no-response), 16384 closed tcp ports (conn-refused)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc?
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Windows 10 Enterprise 19045 microsoft-ds (workgroup: edu)
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49668/tcp open  msrpc        Microsoft Windows RPC
49669/tcp open  msrpc        Microsoft Windows RPC
49675/tcp open  msrpc        Microsoft Windows RPC
49707/tcp open  msrpc        Microsoft Windows RPC
49725/tcp open  msrpc        Microsoft Windows RPC
49925/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: LSHEPHERD; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2024-12-20T13:55:12
|_  start_date: N/A
| smb-os-discovery: 
|   OS: Windows 10 Enterprise 19045 (Windows 10 Enterprise 6.3)
|   OS CPE: cpe:/o:microsoft:windows_10::-
|   Computer name: lshepherd
|   NetBIOS computer name: LSHEPHERD\x00
|   Domain name: edu.stf
|   Forest name: edu.stf
|   FQDN: lshepherd.edu.stf
|_  System time: 2024-12-20T13:55:10+00:00
|_clock-skew: mean: -3s, deviation: 1s, median: -4s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 202.95 seconds

```


Присутсвтует порт 5985 Http
на самом сайте пусто 

#### ❌Samba
Проверил 
закрыто 
(даже учетками с infra-12)
```
[+] IP: 10.154.17.228:445       Name: 10.154.17.228             Status: Authenticated
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        ADMIN$                                                  NO ACCESS       Remote Admin
        C$                                                      NO ACCESS       Default share
        IPC$                                                    READ ONLY       Remote IPC
└─$ smbclient //10.154.17.228/C$ -U sharepoint_spn%killer -W edu.stf --option='client min protocol=SMB2'
tree connect failed: NT_STATUS_ACCESS_DENIED
                                                                                                                  
┌──(kali㉿kali)-[~]
└─$ smbclient //10.154.17.228/C$ -U s_dotson%ricardo -W edu.stf --option='client min protocol=SMB2'   
tree connect failed: NT_STATUS_ACCESS_DENIED

```


#### ❌Feroxbuster Брут директорий
```
feroxbuster  --url  "http://10.154.17.228:5985/" --depth 10 --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-big.txt --status-codes 200,500,401,302,403  --smart 
```
0 директорий Пустота 

#### ❌ почта
думал отправить что то на почту и через фишинг зайти 
l_shepherd
l_shepherd_admin

Вот этим ребятам как дотсону и рикардо, но в ответ тишина ...


---
1. Изучите возможность получения учетных данных из оперативной памяти компьютера. Обратите внимание на возможность сдампить память и изучить ее на наличие учетных данных.
  
2. Проверьте, возможно ли подключиться к другим компьютерам не используя пароль.
  
3. Получите доступ к памяти службы LSASS для выгрузки данных об авторизованных учетных записях.  
Используйте хеш-сумму пароля пользователя L_Shepherd_admin для получения доступа к компьютеру lshepherd.edu.stf.