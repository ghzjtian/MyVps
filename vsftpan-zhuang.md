#vsftp安装
>https://www.vultr.com/docs/setup-vsftpd-on-debian-ubuntu

###[1.安装](#install)
###[2.查看状态](#check_status)
###[3.配置](#setup)
###[4.注意](#attention)
###[5.成功测试例子](#successful_demo)


***
***
***

###1.安装<a name="install"/>
```
root@Tim_s_Server2:~# apt-get install vsftpd
```

***

###2.查看状态<a name="check_status"/>
```
service vsftpd restart
# 查看服务状态
service vsftpd status
#查看端口监听
netstat -nap |grep LISTEN
```

***

###3.配置<a name="setup"/>
```
vim /etc/vsftpd.conf
```
```
#禁止匿名访问(保持默认)
anonymous_enable=NO
#接受本地用户（保持默认）
local_enable=YES
#允许上传
write_enable=YES
#用户只能访问限制的目录
chroot_local_user=YES
local_umask=022
```

* 1.然后重启!



***

###4.注意<a name="attention"/>


```
#As of vsftpd 2.3.5, the chroot directory must not be writable. You can change the permissions of this folder with the following command:

chmod a-w /home/user
```

***
###5.成功测试例子<a name="successful_demo"/>

```
tiandeMacBook-Pro-2:~ tianzeng$ ftp 45.77.19.118
Connected to 45.77.19.118.
220 (vsFTPd 3.0.3)
Name (45.77.19.118:tianzeng): tian
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||14853|)
150 Here comes the directory listing.
drwxrws---    2 0        1001         4096 Nov 12 03:16 scripts
drwxrwsr-x    3 0        1001         4096 Nov 13 01:12 www
226 Directory send OK.
ftp> cd www
250 Directory successfully changed.
ftp> ls
229 Entering Extended Passive Mode (|||46191|)
150 Here comes the directory listing.
drwxr-sr-x    2 1000     1001         4096 Nov 13 01:14 html
226 Directory send OK.
```






