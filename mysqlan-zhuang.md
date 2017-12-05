#Mysql安装
>https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-debian-8
>http://blog.takwolf.com/2016/10/17/setup-mariadb-on-ubuntu/index.html



###* [1.安装](#install)
###* [2.登陆(默认没有密码).](#login)
###* [3.禁止无密码登陆](#forbid_noPsw)
###* [4.卸载](#uninstall)
###* [5.修改密码](#change_psw)
###* [6.配置 mysql 远程访问.](#remoteAccess)
###* [7.基本命令.](#basic_command)


***
***
***

###* 1.安装<a name="install"/>

```
#sudo apt-get install mysql-server
#mysql_secure_installation

#service mysql status
```
***

###* 2.登陆及其他命令(默认没有密码).<a name="login"/>
 
```
#登陆
root@Tim_s_Server2:~# mysql -uroot -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 2
Server version: 10.1.26-MariaDB-0+deb9u1 Debian 9.1
MariaDB [(none)]> 

#查看版本
>* root@Tim_s_Server2:/etc/mysql/mariadb.conf.d# mysql --version   
mysql  Ver 15.1 Distrib 10.1.26-MariaDB, for debian-linux-gnu (x86_64) using readline 5.2


```

###* 3.禁止无密码登陆<a name="forbid_noPsw"/>
>https://stackoverflow.com/questions/44298160/mysql-mariadb-10-0-29-set-root-password-but-still-can-login-without-asking-p

 * 因为是 plugin 设置的问题.
 
 ```
  * SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPass');
  * UPDATE mysql.user SET plugin = '' WHERE user = 'root' AND host = 'localhost';
  * FLUSH PRIVILEGES;
```

***

###* 4.卸载<a name="uninstall"/>
>https://stackoverflow.com/questions/10861374/how-to-remove-mysql-completely-with-config-and-library-files

```
sudo apt-get remove --purge mysql\*
you can delete anything related to packages named mysql. Those commands are only valid on debian / debian-based linux distributions (Ubuntu for example).

You can list all installed mysql packages with the command:

sudo dpkg -l | grep -i mysql
For more cleanup of the package cache, you can use the command:

sudo apt-get clean
Also, remember to use the command:

sudo updatedb
```

***

###* 5.修改密码<a name="change_psw"/>
>https://stackoverflow.com/questions/33467337/reset-mysql-root-password-using-alter-user-statement-after-install-on-mac


***

###* 6.配置 mysql 远程访问.<a name="remoteAccess"/>
* 1.修改配置文件
>https://mariadb.com/kb/zh-cn/configuring-mariadb-for-remote-client-access/
>* 配置文件: /etc/mysql/mariadb.conf.d/50-server.cnf
>


 * 注释以下这行:
 
```
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
#bind-address		= 127.0.0.1
```

* 2.配置 mysql 用户远程登陆权限.
> grant 权限 on 数据库名.表名 to 用户名@登陆方式 identified by 'password1';

 * http://putian.blog.51cto.com/1722818/1287959
 
 ```
 >GRANT ALL PRIVILEGES ON *.* to 'admin'@'%' identified by 'remoteroot123' with grant option;

 #ip地址登陆限制(my-new-password)
 >GRANT ALL PRIVILEGES ON *.* TO 'root'@'218.19.138.%' IDENTIFIED BY 'remoteroot123' WITH GRANT OPTION;
 
 >flush privileges;
 ```

* 3.登陆
 ```
 $ mysql -u root -p -h 45.77.19.118 -P 3306
Enter password: 
 ```

* 4.在 root 用户登陆后，运行以下命令查看效果:

```
MariaDB [(none)]> SELECT User, Host FROM mysql.user;
+-------+-----------+
| User  | Host      |
+-------+-----------+
| admin | %         |
| root  | %         |
| admin | localhost |
| root  | localhost |
+-------+-----------+
4 rows in set (0.00 sec)

```

* 5.取消授权()
>http://chengkinhung.blogspot.com/2013/01/mysql-grantrevoke.html

>revoke 权限 on 数据库名.表名 from 用户名@登陆方式；

```
>revoke all PRIVILEGES ON *.* FROM tian@'%';
>REVOKE GRANT OPTION ON *.* FROM 'tian'@'%';
```
* 6.授权取消后(被禁止了任何的操作):

```
root@glb-gz-debian:/home/tian# mysql -u tian -p
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
+--------------------+
1 row in set (0.00 sec)

mysql> CREATE DATABASE RUNOOB;
ERROR 1044 (42000): Access denied for user 'tian'@'%' to database 'RUNOOB'
```


***


###*7.基本命令<a name="basic_command"/>

* 1.增加用户:
>Add Grant To User after create a user: https://askubuntu.com/questions/461064/unable-to-create-database-due-access-denied

```
#CREATE USER 'tian'@'%' IDENTIFIED BY 'tian1230';
#GRANT ALL PRIVILEGES ON *.* TO 'tian'@'%';
#flush privileges;
```
* 2.增加数据库

```
CREATE DATABASE test; 
#删除 
mysqladmin -u root -p drop RUNOOB
```

* 3.创建表

```
CREATE TABLE IF NOT EXISTS `runoob_tbl`(
   `runoob_id` INT UNSIGNED AUTO_INCREMENT,
   `runoob_title` VARCHAR(100) NOT NULL,
   `runoob_author` VARCHAR(40) NOT NULL,
   `submission_date` DATE,
   PRIMARY KEY ( `runoob_id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```



















