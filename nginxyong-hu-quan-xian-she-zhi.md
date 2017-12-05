#nginx目录用户权限设置

>参考: http://cubicspot.blogspot.com/2017/05/secure-web-server-permissions-that-just.html

###* [1.要实现的功能:](#functions)
###* [2.步骤:](#steps)
###*[3.各种尝试的操作](#other_try)


***
***
***

###* 1.要实现的功能:<a name="functions"/>
* 1.改变 nginx 的网页的主目录
* 2.增加一个用户，实现对主目录的增删查改操作.
* 3.可以随时增加其他用户到该 web 管理组，用户增加后，也可以方便地进行管理操作
* 4.可以实现固定的目录，有固定的用户去管理，该用户不能超出目录的范围.

***

###* 2.步骤:<a name="steps"/>
* 1.增加组(对 webServer 进行管理的组,用 sftp 去操作):
```
root@Tim_s_Server2:~# addgroup sftp-users
Adding group `sftp-users' (GID 1001) ...
Done.
```
* 2.把用户添加到 组里面

```
root@Tim_s_Server2:~# adduser tian sftp-users
Adding user `tian' to group `sftp-users' ...
Adding user tian to group sftp-users
Done.

```

* 3.添加一个目录作为 web server 的主目录
```
#mkdir /home/tian/www
```

* 4.修改文件的权限
```
root@Tim_s_Server2:~# chown root /home/tian/www
root@Tim_s_Server2:~# chgrp sftp-users /home/tian/www
root@Tim_s_Server2:~# chmod 775 /home/tian/www
root@Tim_s_Server2:~# chmod g+s /home/tian/www
```
>```g+s```的解释: >https://unix.stackexchange.com/questions/182212/chmod-gs-command

* 5.增加一个目录，使它可以放置一些用户自定义的任务计划脚本.
```
root@Tim_s_Server2:~# mkdir /home/tian/scripts
root@Tim_s_Server2:~# chown root /home/tian/scripts
root@Tim_s_Server2:~# chgrp sftp-users /home/tian/scripts
root@Tim_s_Server2:~# chmod 770 /home/tian/scripts
root@Tim_s_Server2:~# chmod g+s /home/tian/scripts
```

* 6.如果 web 目录中，有个文件需要特殊的人去管理
```
 chown webAdmin other
```


***

###*3.各种尝试的操作<a name="other_try"/>
* 1.如果把 web 目录中的某个子目录交给另外一个人拥有(不是组内的成员)```chown webAdmin other```,那其他人，包括组的成员，没有写入的权限.
```
tian@Tim_s_Server2:~/www/html$ ls -al
total 72
drwxr-sr-x 3 tian     sftp-users  4096 Nov 12 03:33 .
drwxrwsr-x 4 root     sftp-users  4096 Nov 12 03:27 ..
-rw-r--r-- 1 tian     sftp-users    18 Nov 12 03:30 index.html
drwxr-sr-x 2 webAdmin sftp-users  4096 Nov 12 03:48 other
-rwxr-xr-x 1 tian     sftp-users 56756 Nov 12 03:28 tz.php
tian@Tim_s_Server2:~/www/html$ cd other
tian@Tim_s_Server2:~/www/html/other$ ls -al
total 16
drwxr-sr-x 2 webAdmin sftp-users 4096 Nov 12 03:48 .
drwxr-sr-x 3 tian     sftp-users 4096 Nov 12 03:33 ..
-rw-r--r-- 1 tian     sftp-users   16 Nov 12 03:34 other.html
-rw-r--r-- 1 webAdmin sftp-users   20 Nov 12 03:48 webAdmin.html
tian@Tim_s_Server2:~/www/html/other$ touch tian.html
touch: cannot touch 'tian.html': Permission denied
```

* 2.如果把 web 目录中的某个子目录交给另外一个人拥有(是组内的成员)```chown webAdmin other```,那其他人，包括组的成员，没有写入的权限.

```
root@Tim_s_Server2:/home/tian/www# groups webAdmin2
webAdmin2 : webAdmin2 sftp-users
```

```
tian@Tim_s_Server2:~/www/html/webAdmin2$ ls -al
total 12
drwxr-sr-x 2 webAdmin2 sftp-users 4096 Nov 12 06:06 .
drwxr-sr-x 4 tian      sftp-users 4096 Nov 12 06:06 ..
-rw-r--r-- 1 tian      sftp-users   20 Nov 12 06:06 tian.html
tian@Tim_s_Server2:~/www/html/webAdmin2$ touch tian2.html
touch: cannot touch 'tian2.html': Permission denied
```










