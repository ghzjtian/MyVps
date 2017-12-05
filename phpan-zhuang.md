#php安装

>https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-debian-8

###1.安装
###2.启动
###3.配置 php
###4. 配置 php-fpm
###5.解决 雅黑探针 在 php7.0 现实不全的问题.



***
***
***

###1.安装

```
apt-get install php5-fpm php5-mysql
```
***

###2.启动
```
service php7.0-fpm status
service php7.0-fpm start
/etc/init.d/php7.0-fpm status
```

***

###3.配置 php
>参考: http://www.jianshu.com/p/997a97605ca0

```
vi /etc/php/7.0/fpm/php.ini
```
* 1.让 php 支持 curl(在页面中向其它页面发起请求)
>http://php.net/manual/en/function.curl-init.php
 * 1.安装 curl
 ```
 # apt-cache search curl
 # apt-get install php7.0-curl
 ```
 * 2.删除 php.ini 文件中```;extension=php_curl.dll```前面的 ; ,让其支持 curl .
![](/assets/ScreenShot2017-11-14_14.12.03.png)

***

###4* 配置 php-fpm
```
vi /etc/php/7.0/fpm/pool.d/www.conf
```
***

###5.解决 雅黑探针 在 php7.0 现实不全的问题.
>https://haoyu.love/blog280.html




