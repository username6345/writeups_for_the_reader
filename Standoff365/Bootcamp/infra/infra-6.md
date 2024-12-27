#### Подготовка к атаке
Возвращаясь к заданию №2 infra-2. Напомню в нём мы получили почту через brutforce.
После получения мы отправили письмо  и получили флаг.

Следующий шагом была произведена разведка и были найденные след почтовые ящики (в почтовой контактах ) 
```
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
```
как делать макросы 
генерация revershell https://github.com/glowbase/macro_reverse_shell

 
#### Атака 
t_mathis@edu.stf
getting flag 
```
PS C:\Users\S_Moses_admin> PS C:\Users\S_Moses_admin> Get-ChildItem -Path C:\ -Recurse -Filter hr.txt
    Directory: C:\

Mode                 LastWriteTime         Length Name                                             
----                 -------------         ------ ----                                             
-a----         9/17/2024   7:30 PM             38 hr.txt                                           

    Directory: C:\Program Files\7-Zip\Lang

Mode                 LastWriteTime         Length Name                                             
----                 -------------         ------ ----                                             
-a----         1/28/2018   9:00 AM           8620 hr.txt                                           


PS C:\Users\S_Moses_admin> cat C:\hr.txt
73511420-1d0b-4d67-954e-3f158c4a218a
PS C:\Users\S_Moses_admin>
```


```
PS C:\WINDOWS\system32>  Get-ChildItem -Path C:\ -Recurse -Filter hr.txt 
Directory: C:\


Mode                 LastWriteTime         Length Name                                             
----                 -------------         ------ ----                                             
-a----        11/12/2024   2:30 PM             38 hr.txt                                           


    Directory: C:\Program Files\7-Zip\Lang


Mode                 LastWriteTime         Length Name                                             
----                 -------------         ------ ----                                             
-a----         1/28/2018   9:00 AM           8620 hr.txt                                           


PS C:\WINDOWS\system32> 

    Directory: C:\WINDOWS\system32

```
 