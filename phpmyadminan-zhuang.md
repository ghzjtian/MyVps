#phpMyAdmin安装
>参考: https://ulinuxtips.com/install-phpmyadmin-with-nginx-on-debian-8/


###* 1.安装:

```
apt-get update
apt-get install phpmyadmin
```

***

###* 2.配置
```
#建立链接
ln -s /usr/share/phpmyadmin /var/www/example.com/html
#激活 mcrypt 模块
php5enmod mcrypt
#重启 php
service php7.0-fpm restart
```

***

###* 3.登陆尝试
```
http://example.com/phpmyadmin or ip/phpmyadmin
```

***

###* 4.mysql之"使用配置文件中定义的控制用户连接失败"
>http://www.jianshu.com/p/085851fb8230

