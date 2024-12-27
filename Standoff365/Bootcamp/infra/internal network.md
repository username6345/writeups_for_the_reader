1. Включаем впн_2 который нашли на Infra3
    1. учетки это : учетки почты, но без @...


#### nmap 
##### 40
```
 nmap -sC -sV -p- 10.124.1.240 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-25 11:50 EDT
Nmap scan report for bind.edu.stf (10.124.1.240)
Host is up (0.018s latency).
Not shown: 65532 closed tcp ports (conn-refused)
PORT     STATE SERVICE   VERSION
22/tcp   open  ssh       OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 66:19:7d:a6:e0:77:c1:16:d3:3a:50:13:de:5f:07:41 (RSA)
|   256 d0:e0:da:98:35:58:b3:ce:4a:b1:a6:3f:33:e2:cb:6c (ECDSA)
|_  256 cc:51:46:65:f9:0e:9a:cd:3c:5c:18:56:f9:0b:f5:57 (ED25519)
53/tcp   open  domain    ISC BIND 9.16.48 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.16.48-Ubuntu
1720/tcp open  h323q931?
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 176.55 seconds

```
##### 31
```
 nmap -sC -sV -p- 10.124.1.231       
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-25 13:55 EDT
Nmap scan report for aircraft.edu.stf (10.124.1.231)
Host is up (0.019s latency).
Not shown: 65532 closed tcp ports (conn-refused)
PORT     STATE SERVICE   VERSION
22/tcp   open  ssh       OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 66:19:7d:a6:e0:77:c1:16:d3:3a:50:13:de:5f:07:41 (RSA)
|   256 d0:e0:da:98:35:58:b3:ce:4a:b1:a6:3f:33:e2:cb:6c (ECDSA)
|_  256 cc:51:46:65:f9:0e:9a:cd:3c:5c:18:56:f9:0b:f5:57 (ED25519)
80/tcp   open  http      nginx 1.25.4
|_http-cors: HEAD GET POST
| http-methods: 
|_  Potentially risky methods: PUT PATCH DELETE
|_http-title: Bootstrap Login Form - free examples, templates &amp; tutorial
|_http-server-header: nginx/1.25.4
1720/tcp open  h323q931?
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```
#####  35 36 

```
┌──(kali㉿kali)-[~]
└─$ nmap -sC -sV -p- 10.124.1.235
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-26 12:00 EDT
Nmap scan report for www.edu.stf (10.124.1.235)
Host is up (0.0045s latency).
Not shown: 55527 filtered tcp ports (no-response), 10004 closed tcp ports (conn-refused)
PORT     STATE SERVICE   VERSION
21/tcp   open  ftp       vsftpd 3.0.3
22/tcp   open  ssh       OpenSSH 9.2p1 Debian 2+deb12u1 (protocol 2.0)
| ssh-hostkey: 
|   256 a6:c9:3a:3f:71:4b:ea:7b:0b:55:e9:d5:85:ff:4c:ec (ECDSA)
|_  256 d4:e8:55:8d:31:5c:54:6c:c2:42:c5:49:24:ef:1c:5f (ED25519)
80/tcp   open  http      Apache httpd 2.4.57 ((Debian))
|_http-server-header: Apache/2.4.57 (Debian)
|_http-title: Heavy Logistics
1720/tcp open  h323q931?
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 218.21 seconds
                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ nmap -sC -sV -p- 10.124.1.236
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-26 12:12 EDT
Nmap scan report for gallery.edu.stf (10.124.1.236)
Host is up (0.014s latency).
Not shown: 65532 closed tcp ports (conn-refused)
PORT     STATE SERVICE   VERSION
22/tcp   open  ssh       OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 5f:c7:01:53:89:1a:a8:d5:18:1a:18:1c:9a:d3:50:b1 (RSA)
|   256 e0:cf:fc:04:c4:31:ef:92:1c:53:c8:e0:f5:69:03:6b (ECDSA)
|_  256 57:f5:92:64:3c:1c:26:92:db:51:be:97:a2:c1:e6:1f (ED25519)
80/tcp   open  http      Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.29 (Ubuntu)
1720/tcp open  h323q931?
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 176.32 seconds
                                                              
```

```bash
crackmapexec smb 10.154.16.0/24
SMB         10.154.16.104   445    EXCHANGE         [*] Windows 10 / Server 2019 Build 17763 x64 (name:EXCHANGE) (domain:edu.stf) (signing:True) (SMBv1:False)
SMB         10.154.16.105   445    MSSQL            [*] Windows 10 / Server 2019 Build 17763 x64 (name:MSSQL) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.100   445    LOGC             [*] Windows 10 / Server 2019 Build 17763 x64 (name:LOGC) (domain:logc) (signing:False) (SMBv1:False)
SMB         10.154.16.106   445    SHPOINT          [*] Windows 10 / Server 2019 Build 17763 x64 (name:SHPOINT) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.107   445    BACKUP           [*] Windows 10 / Server 2019 Build 17763 x64 (name:BACKUP) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.135   445    DC-2             [*] Windows Server 2016 Standard 14393 x64 (name:DC-2) (domain:edu.stf) (signing:True) (SMBv1:True)
SMB         10.154.16.134   445    DC               [*] Windows Server 2016 Standard 14393 x64 (name:DC) (domain:edu.stf) (signing:True) (SMBv1:True)
SMB         10.154.16.204   445    MMCDOWELL        [*] Windows 7 Ultimate 7601 Service Pack 1 x64 (name:MMCDOWELL) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.203   445    CBLAIR           [*] Windows 10 Enterprise 19045 x64 (name:CBLAIR) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.202   445    JHEBERT          [*] Windows 7 Ultimate 7601 Service Pack 1 x64 (name:JHEBERT) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.197   445    TMATHIS          [*] Windows 10 Enterprise 19045 x64 (name:TMATHIS) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.208   445    MHOLDEN          [*] Windows 10 Enterprise 19045 x64 (name:MHOLDEN) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.198   445    CFRAZIER         [*] Windows 10 Enterprise 19045 x64 (name:CFRAZIER) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.205   445    GRODRIQUEZ       [*] Windows 10 Enterprise 19045 x64 (name:GRODRIQUEZ) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.201   445    LBLACKBURN       [*] Windows 10 Enterprise 19045 x64 (name:LBLACKBURN) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.196   445    SDOTSON          [*] Windows 10 Enterprise 19045 x64 (name:SDOTSON) (domain:edu.stf) (signing:False) (SMBv1:True)

```

 

```
crackmapexec smb 10.154.16.0/24 -u user -p pass
SMB         10.154.16.105   445    MSSQL            [*] Windows 10 / Server 2019 Build 17763 x64 (name:MSSQL) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.100   445    LOGC             [*] Windows 10 / Server 2019 Build 17763 x64 (name:LOGC) (domain:logc) (signing:False) (SMBv1:False)
SMB         10.154.16.104   445    EXCHANGE         [*] Windows 10 / Server 2019 Build 17763 x64 (name:EXCHANGE) (domain:edu.stf) (signing:True) (SMBv1:False)
SMB         10.154.16.105   445    MSSQL            [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.105   445    MSSQL            [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.100   445    LOGC             [-] logc\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.106   445    SHPOINT          [*] Windows 10 / Server 2019 Build 17763 x64 (name:SHPOINT) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.100   445    LOGC             [-] logc\s_dotson:ricardo STATUS_LOGON_FAILURE 
SMB         10.154.16.100   445    LOGC             [-] logc\r_andrews:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.100   445    LOGC             [-] logc\r_andrews:ricardo STATUS_LOGON_FAILURE 
SMB         10.154.16.107   445    BACKUP           [*] Windows 10 / Server 2019 Build 17763 x64 (name:BACKUP) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.106   445    SHPOINT          [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.106   445    SHPOINT          [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.104   445    EXCHANGE         [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.104   445    EXCHANGE         [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.107   445    BACKUP           [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.107   445    BACKUP           [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.135   445    DC-2             [*] Windows Server 2016 Standard 14393 x64 (name:DC-2) (domain:edu.stf) (signing:True) (SMBv1:True)
SMB         10.154.16.134   445    DC               [*] Windows Server 2016 Standard 14393 x64 (name:DC) (domain:edu.stf) (signing:True) (SMBv1:True)
SMB         10.154.16.135   445    DC-2             [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.135   445    DC-2             [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.134   445    DC               [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.134   445    DC               [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.198   445    CFRAZIER         [*] Windows 10 Enterprise 19045 x64 (name:CFRAZIER) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.196   445    SDOTSON          [*] Windows 10 Enterprise 19045 x64 (name:SDOTSON) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.197   445    TMATHIS          [*] Windows 10 Enterprise 19045 x64 (name:TMATHIS) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.202   445    JHEBERT          [*] Windows 7 Ultimate 7601 Service Pack 1 x64 (name:JHEBERT) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.203   445    CBLAIR           [*] Windows 10 Enterprise 19045 x64 (name:CBLAIR) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.208   445    MHOLDEN          [*] Windows 10 Enterprise 19045 x64 (name:MHOLDEN) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.204   445    MMCDOWELL        [*] Windows 7 Ultimate 7601 Service Pack 1 x64 (name:MMCDOWELL) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.205   445    GRODRIQUEZ       [*] Windows 10 Enterprise 19045 x64 (name:GRODRIQUEZ) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.201   445    LBLACKBURN       [*] Windows 10 Enterprise 19045 x64 (name:LBLACKBURN) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.198   445    CFRAZIER         [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.198   445    CFRAZIER         [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.196   445    SDOTSON          [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.196   445    SDOTSON          [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.197   445    TMATHIS          [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.197   445    TMATHIS          [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.202   445    JHEBERT          [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.202   445    JHEBERT          [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.203   445    CBLAIR           [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.203   445    CBLAIR           [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.208   445    MHOLDEN          [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.208   445    MHOLDEN          [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.204   445    MMCDOWELL        [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.204   445    MMCDOWELL        [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.205   445    GRODRIQUEZ       [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.205   445    GRODRIQUEZ       [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.201   445    LBLACKBURN       [-] edu.stf\s_dotson:dancer STATUS_LOGON_FAILURE 
SMB         10.154.16.201   445    LBLACKBURN       [+] edu.stf\s_dotson:ricardo 

```



```

└─$ nmap -sV -T5 10.154.16.107 -vvv
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-26 13:27 EST
NSE: Loaded 46 scripts for scanning.
Initiating Ping Scan at 13:27
Scanning 10.154.16.107 [2 ports]
Completed Ping Scan at 13:27, 0.01s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 13:27
Completed Parallel DNS resolution of 1 host. at 13:27, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 13:27
Scanning 10.154.16.107 [1000 ports]
Discovered open port 3389/tcp on 10.154.16.107
Discovered open port 445/tcp on 10.154.16.107
Discovered open port 1720/tcp on 10.154.16.107
Discovered open port 135/tcp on 10.154.16.107
Discovered open port 139/tcp on 10.154.16.107
Completed Connect Scan at 13:27, 1.32s elapsed (1000 total ports)
Initiating Service scan at 13:27
Scanning 5 services on 10.154.16.107
Stats: 0:00:47 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 60.00% done; ETC: 13:28 (0:00:31 remaining)
Stats: 0:00:55 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 60.00% done; ETC: 13:28 (0:00:35 remaining)
Service scan Timing: About 80.00% done; ETC: 13:30 (0:00:39 remaining)
Completed Service scan at 13:30, 156.49s elapsed (5 services on 1 host)
NSE: Script scanning 10.154.16.107.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 13:30
Completed NSE at 13:30, 0.01s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 13:30
Completed NSE at 13:30, 1.02s elapsed
Nmap scan report for 10.154.16.107
Host is up, received conn-refused (0.0069s latency).
Scanned at 2024-11-26 13:27:22 EST for 159s
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE       REASON  VERSION
135/tcp  open  msrpc?        syn-ack
139/tcp  open  netbios-ssn   syn-ack Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds? syn-ack
1720/tcp open  h323q931?     syn-ack
3389/tcp open  ms-wbt-server syn-ack Microsoft Terminal Services
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 159.05 seconds

```

 

```
nmap -Pn -p- 10.154.16.134
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-17 11:05 EST
Nmap scan report for 10.154.16.134
Host is up (0.015s latency).
Not shown: 49138 filtered tcp ports (no-response), 16375 closed tcp ports (conn-refused)
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49668/tcp open  unknown
49671/tcp open  unknown
49675/tcp open  unknown
49676/tcp open  unknown
49680/tcp open  unknown
49694/tcp open  unknown
49776/tcp open  unknown

```


#### 134

```
./kerbrute  userenum --dc 10.154.16.134 -d edu.stf /usr/share/wordlists/rockyou.txt

    __             __               __     
   / /_____  _____/ /_  _______  __/ /____ 
  / //_/ _ \/ ___/ __ \/ ___/ / / / __/ _ \
 / ,< /  __/ /  / /_/ / /  / /_/ / /_/  __/
/_/|_|\___/_/  /_.___/_/   \__,_/\__/\___/                                        

Version: dev (n/a) - 12/18/24 - Ronnie Flathers @ropnop

2024/12/18 07:35:12 >  Using KDC(s):
2024/12/18 07:35:12 >   10.154.16.134:88

2024/12/18 07:35:39 >  [+] VALID USERNAME:       administrator@edu.stf
2024/12/18 07:36:22 >  [+] VALID USERNAME:       backup@edu.stf
2024/12/18 07:36:59 >  [+] VALID USERNAME:       exchange@edu.stf
2024/12/18 07:49:15 >  [+] VALID USERNAME:       ekelly@edu.stf
2024/12/18 08:02:02 >  [+] VALID USERNAME:       Administrator@edu.stf
2024/12/18 08:25:14 >  [+] VALID USERNAME:       dc@edu.stf
2024/12/18 08:34:13 >  [+] VALID USERNAME:       ADMINISTRATOR@edu.stf

2024/12/18 09:18:40 >  [+] VALID USERNAME:       smoses@edu.stf

   

```

```
 nslookup shpoint.edu.stf 10.154.16.134                 
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   shpoint.edu.stf
Address: 10.154.16.106


```

```
└─$ dig @10.154.16.134 edu.stf NS

; <<>> DiG 9.19.21-1-Debian <<>> @10.154.16.134 edu.stf NS
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 33019
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 3

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4000
;; QUESTION SECTION:
;edu.stf.                       IN      NS

;; ANSWER SECTION:
edu.stf.                3600    IN      NS      dc-2.edu.stf.
edu.stf.                3600    IN      NS      dc.edu.stf.

;; ADDITIONAL SECTION:
dc-2.edu.stf.           3600    IN      A       10.154.16.135
dc.edu.stf.             3600    IN      A       10.154.16.134

;; Query time: 8 msec
;; SERVER: 10.154.16.134#53(10.154.16.134) (UDP)
;; WHEN: Tue Dec 17 11:27:35 EST 2024
;; MSG SIZE  rcvd: 104

```


```
 nmap -sV -Pn 10.154.16.134
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-18 07:46 EST
Nmap scan report for 10.154.16.134
Host is up (0.012s latency).
Not shown: 935 filtered tcp ports (no-response), 55 closed tcp ports (conn-refused)
PORT     STATE SERVICE      VERSION
53/tcp   open  domain       Simple DNS Plus
88/tcp   open  kerberos-sec Microsoft Windows Kerberos (server time: 2024-12-18 12:47:05Z)
135/tcp  open  msrpc?
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
389/tcp  open  ldap         Microsoft Windows Active Directory LDAP (Domain: edu.stf, Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds (workgroup: edu)
464/tcp  open  kpasswd5?
636/tcp  open  ssl/ldap     Microsoft Windows Active Directory LDAP (Domain: edu.stf, Site: Default-First-Site-Name)
3268/tcp open  ldap         Microsoft Windows Active Directory LDAP (Domain: edu.stf, Site: Default-First-Site-Name)
3269/tcp open  ssl/ldap     Microsoft Windows Active Directory LDAP (Domain: edu.stf, Site: Default-First-Site-Name)
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 161.61 seconds

```


####  другое 
```
nmap 10.154.16.1 -Pn   
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-18 04:20 EST
Verbosity Increased to 1.
Verbosity Increased to 2.
Verbosity Increased to 3.
Connect Scan Timing: About 15.50% done; ETC: 04:24 (0:02:49 remaining)
Connect Scan Timing: About 30.50% done; ETC: 04:24 (0:02:19 remaining)
Completed Connect Scan at 04:22, 83.16s elapsed (1000 total ports)
Nmap scan report for 10.154.16.1
Host is up (0.014s latency).
Scanned at 2024-12-18 04:20:54 EST for 83s
Not shown: 997 filtered tcp ports (no-response)
PORT     STATE  SERVICE
264/tcp  closed bgmp
444/tcp  closed snpp
8082/tcp closed blackice-alerts

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 83.19 seconds


Nmap scan report for 10.154.16.13
Host is up (0.025s latency).
Scanned at 2024-12-18 04:56:16 EST for 402s
Not shown: 999 filtered tcp ports (no-response)
PORT     STATE SERVICE
8443/tcp open  https-alt

```


```
Nmap scan report for 10.154.16.33
Host is up (0.012s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT     STATE  SERVICE
264/tcp  closed bgmp
444/tcp  closed snpp
8082/tcp closed blackice-alerts

```



```

 

Nmap scan report for 10.154.16.65
Host is up (0.013s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE
22/tcp   open  ssh
256/tcp  open  fw1-secureremote
443/tcp  open  https
900/tcp  open  omginitialrefs
1720/tcp open  h323q931
8082/tcp open  blackice-alerts

 
```
65 443

![[Pasted image 20241218143411.png]]

```
Nmap scan report for 10.154.16.74
Host is up (0.012s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE
22/tcp   open  ssh
25/tcp   open  smtp
80/tcp   open  http
443/tcp  open  https
1720/tcp open  h323q931

```
на 443 находиться gitlab что молчит 



на 80 просто две буквы `tr`
``` 
Nmap scan report for 10.154.16.75
Host is up (0.011s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
1720/tcp open  h323q931
3301/tcp open  tarantool
```


```
Nmap scan report for 10.154.16.76
Host is up (0.020s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
1720/tcp open  h323q931
5432/tcp open  postgresql
8080/tcp open  http-proxy

 

Nmap scan report for 10.154.16.97
Host is up (0.012s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE    SERVICE
22/tcp   filtered ssh
80/tcp   filtered http
256/tcp  open     fw1-secureremote
443/tcp  filtered https
900/tcp  filtered omginitialrefs
1720/tcp open     h323q931

 

Nmap scan report for 10.154.16.100
Host is up (0.012s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

```


```
Nmap scan report for 10.154.16.100
Host is up (0.0088s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

```

```
exchange.edu.stf
Nmap scan report for 10.154.16.104
Host is up (0.0089s latency).
Not shown: 972 closed tcp ports (conn-refused)
PORT     STATE SERVICE
25/tcp   open  smtp
80/tcp   open  http
81/tcp   open  hosts2-ns
110/tcp  open  pop3
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
143/tcp  open  imap
443/tcp  open  https
444/tcp  open  snpp
445/tcp  open  microsoft-ds
465/tcp  open  smtps
587/tcp  open  submission
593/tcp  open  http-rpc-epmap
808/tcp  open  ccproxy-http
993/tcp  open  imaps
995/tcp  open  pop3s
1720/tcp open  h323q931
1801/tcp open  msmq
2103/tcp open  zephyr-clt
2105/tcp open  eklogin
2107/tcp open  msmq-mgmt
2525/tcp open  ms-v-worlds
3389/tcp open  ms-wbt-server
3800/tcp open  pwgpsi
3801/tcp open  ibm-mgr
3828/tcp open  neteh
6001/tcp open  X11:1
6510/tcp open  mcer-port

```

```
Nmap scan report for 10.154.16.105
Host is up (0.0093s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
1433/tcp open  ms-sql-s
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

Nmap scan report for 10.154.16.106
Host is up (0.015s latency).
Not shown: 993 closed tcp ports (conn-refused)
PORT     STATE SERVICE
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
808/tcp  open  ccproxy-http
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

Nmap scan report for 10.154.16.107
Host is up (0.0091s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

```


```
Nmap scan report for 10.154.16.135
Host is up (0.015s latency).
Not shown: 935 filtered tcp ports (no-response), 55 closed tcp ports (conn-refused)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
636/tcp  open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl

```


```
Nmap scan report for 10.154.16.193
Host is up (0.0095s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE    SERVICE
22/tcp   filtered ssh
80/tcp   filtered http
256/tcp  open     fw1-secureremote
443/tcp  filtered https
900/tcp  filtered omginitialrefs
1720/tcp open     h323q931

```

```
Nmap scan report for 10.154.16.196
Host is up (0.015s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
443/tcp  open  https
445/tcp  open  microsoft-ds
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

Nmap scan report for 10.154.16.197
Host is up (0.014s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
443/tcp  open  https
445/tcp  open  microsoft-ds
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

Nmap scan report for 10.154.16.198
Host is up (0.013s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
443/tcp  open  https
445/tcp  open  microsoft-ds
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

```


```

Nmap scan report for 10.154.16.201
Host is up (0.014s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
443/tcp  open  https
445/tcp  open  microsoft-ds
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

Nmap scan report for 10.154.16.202
Host is up (0.013s latency).
Not shown: 991 closed tcp ports (conn-refused)
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
443/tcp   open  https
445/tcp   open  microsoft-ds
1720/tcp  open  h323q931
3389/tcp  open  ms-wbt-server
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown

Nmap scan report for 10.154.16.203
Host is up (0.014s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
443/tcp  open  https
445/tcp  open  microsoft-ds
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server


```

```
Nmap scan report for 10.154.16.204
Host is up (0.016s latency).
Not shown: 989 closed tcp ports (conn-refused)
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
443/tcp   open  https
445/tcp   open  microsoft-ds
1720/tcp  open  h323q931
3389/tcp  open  ms-wbt-server
5357/tcp  open  wsdapi
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49163/tcp open  unknown

Nmap scan report for 10.154.16.205
Host is up (0.014s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
443/tcp  open  https
445/tcp  open  microsoft-ds
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

```


```
Nmap scan report for 10.154.16.208
Host is up (0.016s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
443/tcp  open  https
445/tcp  open  microsoft-ds
1720/tcp open  h323q931
3389/tcp open  ms-wbt-server

```


#### соответствие домена и айпи

```
nslookup  sdotson.edu.stf 10.154.16.134       
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   sdotson.edu.stf
Address: 10.154.16.196



└─$ nslookup  lshepherd.edu.stf  10.154.16.134                                                    
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   lshepherd.edu.stf
Address: 10.154.17.228

                                                                                                                  
┌──(kali㉿kali)-[~]
└─$ nslookup  mssql.edu.stf 10.154.16.134            
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   mssql.edu.stf
Address: 10.154.16.105

                                                                                                                  
┌──(kali㉿kali)-[~]
└─$ nslookup  smoses.edu.stf 10.154.16.134       
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   smoses.edu.stf
Address: 10.154.17.229

                                                                                                                  
┌──(kali㉿kali)-[~]
└─$ nslookup  hmorgan.edu.stf 10.154.16.134       
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   hmorgan.edu.stf
Address: 10.154.17.231

                                                                                                                  
┌──(kali㉿kali)-[~]
└─$ nslookup  dc-2.edu.stf 10.154.16.134          
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   dc-2.edu.stf
Address: 10.154.16.135

                                                                                                                  
┌──(kali㉿kali)-[~]
└─$ nslookup  dc.edu.stf 10.154.16.134        
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   dc.edu.stf
Address: 10.154.16.134

```


#### smb

```bash
 crackmapexec smb  10.154.16.0/24 -u s_dotson -p ricardo

SMB         10.154.16.105   445    MSSQL            [*] Windows 10 / Server 2019 Build 17763 x64 (name:MSSQL) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.104   445    EXCHANGE         [*] Windows 10 / Server 2019 Build 17763 x64 (name:EXCHANGE) (domain:edu.stf) (signing:True) (SMBv1:False)
SMB         10.154.16.100   445    LOGC             [*] Windows 10 / Server 2019 Build 17763 x64 (name:LOGC) (domain:logc) (signing:False) (SMBv1:False)
SMB         10.154.16.105   445    MSSQL            [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.106   445    SHPOINT          [*] Windows 10 / Server 2019 Build 17763 x64 (name:SHPOINT) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.104   445    EXCHANGE         [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.100   445    LOGC             [-] logc\s_dotson:ricardo STATUS_LOGON_FAILURE 
SMB         10.154.16.107   445    BACKUP           [*] Windows 10 / Server 2019 Build 17763 x64 (name:BACKUP) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.106   445    SHPOINT          [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.107   445    BACKUP           [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.135   445    DC-2             [*] Windows Server 2016 Standard 14393 x64 (name:DC-2) (domain:edu.stf) (signing:True) (SMBv1:True)
SMB         10.154.16.134   445    DC               [*] Windows Server 2016 Standard 14393 x64 (name:DC) (domain:edu.stf) (signing:True) (SMBv1:True)
SMB         10.154.16.135   445    DC-2             [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.134   445    DC               [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.201   445    LBLACKBURN       [*] Windows 10 Enterprise 19045 x64 (name:LBLACKBURN) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.202   445    JHEBERT          [*] Windows 7 Ultimate 7601 Service Pack 1 x64 (name:JHEBERT) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.208   445    MHOLDEN          [*] Windows 10 Enterprise 19045 x64 (name:MHOLDEN) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.196   445    SDOTSON          [*] Windows 10 Enterprise 19045 x64 (name:SDOTSON) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.198   445    CFRAZIER         [*] Windows 10 Enterprise 19045 x64 (name:CFRAZIER) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.203   445    CBLAIR           [*] Windows 10 Enterprise 19045 x64 (name:CBLAIR) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.197   445    TMATHIS          [*] Windows 10 Enterprise 19045 x64 (name:TMATHIS) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.205   445    GRODRIQUEZ       [*] Windows 10 Enterprise 19045 x64 (name:GRODRIQUEZ) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.204   445    MMCDOWELL        [*] Windows 7 Ultimate 7601 Service Pack 1 x64 (name:MMCDOWELL) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.201   445    LBLACKBURN       [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.202   445    JHEBERT          [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.208   445    MHOLDEN          [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.196   445    SDOTSON          [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.203   445    CBLAIR           [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.198   445    CFRAZIER         [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.197   445    TMATHIS          [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.205   445    GRODRIQUEZ       [+] edu.stf\s_dotson:ricardo 
SMB         10.154.16.204   445    MMCDOWELL        [+] edu.stf\s_dotson:ricardo 

```


#### mail Почты

https://10.154.16.104/owa/auth/logon.aspx?replaceCurrent=1&reason=2&url=https%3a%2f%2f10.154.16.104%2fowa%2f

```
cat ldap.txt |  grep mail:   
mail: Administrator@edu.stf
mail: l_blackburn@edu.stf
mail: s_dotson@edu.stf
mail: j_hebert@edu.stf
mail: t_mathis@edu.stf
mail: c_blair@edu.stf
mail: h_morgan@edu.stf
mail: m_mcdowell@edu.stf
mail: l_shepherd@edu.stf
mail: e_kelly@edu.stf
mail: s_moses@edu.stf
mail: h_morgan@edu.stf
mail: l_shepherd@edu.stf
mail: e_kelly@edu.stf
mail: s_moses@edu.stf
mail: vpn@edu.stf
mail: sp_admin@edu.stf
mail: exchange@edu.stf
mail: SystemMailbox{1f05a927-be4e-425f-a728-4eb24a89a632}@edu.stf
mail: SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}@edu.stf
mail: SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}@edu.stf
mail: DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}@edu.stf
mail: Migration.8f3e7716-2011-43e4-96b1-aba62d229136@edu.stf
mail: FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042@edu.stf
mail: SystemMailbox{D0E409A0-AF9B-4720-92FE-AAC869B0D201}@edu.stf
mail: SystemMailbox{2CE34405-31BE-455D-89D7-A7C7DA7A0DAA}@edu.stf
mail: SystemMailbox{8cc370d3-822a-4ab8-a926-bb94bd0641a9}@edu.stf
mail: HealthMailbox02152e70d5124fa0bb95186906c0d81b@edu.stf
mail: HealthMailbox16f4d63e58fc40918c9f62671bf5c43e@edu.stf
mail: HealthMailbox8f46d57707c5484f858a646207b95e59@edu.stf
mail: HealthMailbox6e2c32a1aa8b484095d15c22c15e7e4c@edu.stf
mail: HealthMailboxa3df24edcb7d4e54bc0689860513e500@edu.stf
mail: HealthMailbox0d7656f4d87140b69da8b8c77ce1cab8@edu.stf
mail: HealthMailboxb7326a7976d443d2b3dd35c2bc81590c@edu.stf
mail: HealthMailbox76f2f356b1324548855aca203198774d@edu.stf
mail: HealthMailbox05d53f7d85b5403687212ab66a2c37be@edu.stf
mail: HealthMailbox5782d38e97cf40e4a2889c073875de81@edu.stf
mail: HealthMailbox74bcea7372934362a4b9eb6312f71ee5@edu.stf
mail: m_holden@edu.stf
mail: g_rodriquez@edu.stf
mail: gitlab@edu.stf
mail: r_andrews@edu.stf
mail: getmailflag@edu.stf

```


#### 17 сетка 


```
└─$  nmap -sV -Pn  -p- 10.154.17.228
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-21 06:57 EST
Nmap scan report for 10.154.17.228
Host is up (0.011s latency).
Not shown: 49138 filtered tcp ports (no-response), 16384 closed tcp ports (conn-refused)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc?
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: edu)
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
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

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 338.00 seconds


 nmap -sV -Pn  -p- 10.154.17.229
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-21 06:57 EST
Nmap scan report for 10.154.17.229
Host is up (0.013s latency).
Not shown: 49138 filtered tcp ports (no-response), 16384 closed tcp ports (conn-refused)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc?
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: edu)
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49461/tcp open  msrpc        Microsoft Windows RPC
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49668/tcp open  msrpc        Microsoft Windows RPC
49669/tcp open  msrpc        Microsoft Windows RPC
49673/tcp open  msrpc        Microsoft Windows RPC
49696/tcp open  msrpc        Microsoft Windows RPC
49702/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: SMOSES; OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 314.76 seconds
                                                              
 

 nmap -sV -Pn  -p- 10.154.17.231                            
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-21 06:57 EST
Nmap scan report for 10.154.17.231
Host is up (0.012s latency).
Not shown: 49138 filtered tcp ports (no-response), 16384 closed tcp ports (conn-refused)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc?
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: edu)
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49668/tcp open  msrpc        Microsoft Windows RPC
49669/tcp open  msrpc        Microsoft Windows RPC
49671/tcp open  msrpc        Microsoft Windows RPC
49693/tcp open  msrpc        Microsoft Windows RPC
49714/tcp open  msrpc        Microsoft Windows RPC
63700/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: HMORGAN; OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 262.47 seconds


nmap -sV -Pn  -p- 10.154.17.232
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-21 06:57 EST
Nmap scan report for 10.154.17.232
Host is up (0.012s latency).
Not shown: 49138 filtered tcp ports (no-response), 16384 closed tcp ports (conn-refused)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc?
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: edu)
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49668/tcp open  msrpc        Microsoft Windows RPC
49670/tcp open  msrpc        Microsoft Windows RPC
49671/tcp open  msrpc        Microsoft Windows RPC
49682/tcp open  msrpc        Microsoft Windows RPC
49717/tcp open  msrpc        Microsoft Windows RPC
65468/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: EKELLY; OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 373.08 seconds
                                                               

```


#### ldap
```
ldapdomaindump -u "lshepherd.edu.stf\s_dotson" -p 'ricardo' 10.154.16.135
```