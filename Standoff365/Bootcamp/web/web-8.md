1. Чтение файлов через функцию загрузки по URL:  
  
Используйте функцию загрузки новых картинок в галерее через URL.  
Уязвимость может возникнуть из-за использования функции copy() без должной фильтрации.  
Есть возможность скопировать произвольный файл в папку images с расширением txt и затем прочитать его. Примеры payload:  
file:///etc/passwd  
./ajax.php  
./classes.php

2. Использование метода __destruct в классе ImageSorting:  
  
Обратите внимание на метод __destruct в классе ImageSorting, который вызывается при уничтожении объекта.  
Этот метод позволяет перезаписать переменные $ImageArr и $SortFunc, которые в дальнейшем используются в функции usort() для сортировки массива.  
Есть возможность прочитать файл classes.php, создать phar-архив с объектом, который модифицирует переменные таким образом, чтобы они вызвали выполнение произвольного кода при десериализации.

3. Эксплуатация десериализации через созданный phar-архив:  
  
Создайте phar-архив с объектом, который перезаписывает переменные $ImageArr и $SortFunc.  
Используйте загрузку по URL в галерее, чтобы загрузить созданный phar-архив.  
При загрузке архива происходит его десериализация, что приводит к выполнению произвольного кода из $SortFunc.  
Убедитесь, что переменная $SortFunc установлена на system, чтобы выполнять системные команды.


#### scout
```
└─$ nmap -p- -T5 10.124.1.236                         
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-28 11:18 EDT
Nmap scan report for gallery.edu.stf (10.124.1.236)
Host is up (0.020s latency).
Not shown: 65532 closed tcp ports (conn-refused)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
1720/tcp open  h323q931

```