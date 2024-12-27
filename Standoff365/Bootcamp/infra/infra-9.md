[Bootcamp standoff365](Ответы%20решений%20заданий/Standoff/Bootcamp%20standoff365.md)
#### Цель
Получите доступ к серверу **backup.edu.stf** и к содержимому файла flag.txt.


```
SMB         10.154.16.105   445    MSSQL            [*] Windows 10.0 Build 17763 x64 (name:MSSQL) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.100   445    LOGC             [*] Windows 10.0 Build 17763 x64 (name:LOGC) (domain:logc) (signing:False) (SMBv1:False)
SMB         10.154.16.104   445    EXCHANGE         [*] Windows 10.0 Build 17763 x64 (name:EXCHANGE) (domain:edu.stf) (signing:True) (SMBv1:False)
SMB         10.154.16.106   445    SHPOINT          [*] Windows 10.0 Build 17763 x64 (name:SHPOINT) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.107   445    BACKUP           [*] Windows 10.0 Build 17763 x64 (name:BACKUP) (domain:edu.stf) (signing:False) (SMBv1:False)
SMB         10.154.16.134   445    DC               [*] Windows Server 2016 Standard 14393 x64 (name:DC) (domain:edu.stf) (signing:True) (SMBv1:True)
SMB         10.154.16.135   445    DC-2             [*] Windows Server 2016 Standard 14393 x64 (name:DC-2) (domain:edu.stf) (signing:True) (SMBv1:True)
SMB         10.154.16.197   445    TMATHIS          [*] Windows 10 Enterprise 19045 x64 (name:TMATHIS) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.203   445    CBLAIR           [*] Windows 10 Enterprise 19045 x64 (name:CBLAIR) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.198   445    CFRAZIER         [*] Windows 10 Enterprise 19045 x64 (name:CFRAZIER) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.202   445    JHEBERT          [*] Windows 7 Ultimate 7601 Service Pack 1 x64 (name:JHEBERT) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.201   445    LBLACKBURN       [*] Windows 10 Enterprise 19045 x64 (name:LBLACKBURN) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.204   445    MMCDOWELL        [*] Windows 7 Ultimate 7601 Service Pack 1 x64 (name:MMCDOWELL) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.205   445    GRODRIQUEZ       [*] Windows 10 Enterprise 19045 x64 (name:GRODRIQUEZ) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.208   445    MHOLDEN          [*] Windows 10 Enterprise 19045 x64 (name:MHOLDEN) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.16.196   445    SDOTSON          [*] Windows 10 Enterprise 19045 x64 (name:SDOTSON) (domain:edu.stf) (signing:False) (SMBv1:True)
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ crackmapexec smb  10.154.17.0/24

SMB         10.154.17.229   445    SMOSES           [*] Windows 10 Enterprise 19045 x64 (name:SMOSES) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.17.231   445    HMORGAN          [*] Windows 10 Enterprise 19045 x64 (name:HMORGAN) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.17.232   445    EKELLY           [*] Windows 10 Enterprise 19045 x64 (name:EKELLY) (domain:edu.stf) (signing:False) (SMBv1:True)
SMB         10.154.17.228   445    LSHEPHERD        [*] Windows 10 Enterprise 19045 x64 (name:LSHEPHERD) (domain:edu.stf) (signing:False) (SMBv1:True)

```


```
nslookup  backup.edu.stf 10.154.16.134              
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   backup.edu.stf
Address: 10.154.16.107
```


```
nmap -sV -Pn -p- -A -T5  10.154.16.107    
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-19 13:58 EST
Warning: 10.154.16.107 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.154.16.107
Host is up (0.018s latency).
Not shown: 65518 closed tcp ports (conn-refused)
PORT      STATE    SERVICE       VERSION
135/tcp   open     msrpc?
139/tcp   open     netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open     microsoft-ds?
1720/tcp  open     h323q931?
3389/tcp  open     ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=backup.edu.stf
| Not valid before: 2024-07-18T10:56:23
|_Not valid after:  2025-01-17T10:56:23
| rdp-ntlm-info: 
|   Target_Name: edu
|   NetBIOS_Domain_Name: edu
|   NetBIOS_Computer_Name: BACKUP
|   DNS_Domain_Name: edu.stf
|   DNS_Computer_Name: backup.edu.stf
|   DNS_Tree_Name: edu.stf
|   Product_Version: 10.0.17763
|_  System_Time: 2024-12-19T19:01:24+00:00
|_ssl-date: 2024-12-19T19:01:52+00:00; -4s from scanner time.
5985/tcp  open     http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open     http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open     msrpc         Microsoft Windows RPC
49665/tcp open     msrpc         Microsoft Windows RPC
49667/tcp open     msrpc         Microsoft Windows RPC
49669/tcp open     msrpc         Microsoft Windows RPC
49670/tcp open     msrpc         Microsoft Windows RPC
49682/tcp open     msrpc         Microsoft Windows RPC
49708/tcp open     msrpc         Microsoft Windows RPC
49710/tcp open     msrpc         Microsoft Windows RPC
49750/tcp open     msrpc         Microsoft Windows RPC
61730/tcp filtered unknown
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
|_clock-skew: mean: -3s, deviation: 0s, median: -3s
| smb2-time: 
|   date: 2024-12-19T19:01:26
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 195.29 seconds

```


  
1. Просканируйте узел на наличие уязвимостей.
2.   
2. Обратите внимание на запущенные службы на узле.
3.   
3. Изучите уязвимость PrintNightmare и проэксплуатируйте ее на узле.


printnightmare CVE-2021-34527 https://github.com/LaresLLC/CVE-2021-1675


CVE-2021-1675 и дополнительный эксплойт удаленного выполнения кода в службе диспетчера очереди печати Windows, известный как “PrintNightmare”, задокументированный в CVE-2021-34527.



#### Возможные векторы атак

```
python3 rpcdump.py 10.154.16.107 -p 135 | egrep 'MS-RPRN|MS-PAR'
Protocol: [MS-PAR]: Print System Asynchronous Remote Protocol 
Protocol: [MS-RPRN]: Print System Remote Protocol 
```

https://juggernaut-sec.com/ad-recon-msrpc/

тут именно о ней https://juggernaut-sec.com/printnightmare/

https://github.com/cube0x0/CVE-2021-1675
https://mayfly277.github.io/posts/GOADv2-pwning-part5/

#### имена

```
rpcclient -U "guest"  10.154.16.107
rpcclient -U "backup"  10.154.16.107

```

