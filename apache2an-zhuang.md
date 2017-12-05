#Nginx安装
>1.https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-debian-8
>2.server name : japanvps.com



***
***
***


###1.查看包的状态

```
aptitude search nginx

```

###[2.安装](#install)

###[3.启动/停止](#start_command)
###[4.查看php配置文件目录](#search_directory)
###6.网站目录
```
/var/www/html
```
###[7.配置Nginx至支持PHP](#support_php)
###8.配置文件

```
root@Tim_s_Server2:~# find / -name 'nginx.conf'
/etc/init/nginx.conf
/etc/nginx/nginx.conf
```

###[9.更改 nginx 的默认 www 路径.](#change_default_directory)

***
***
***

###2.安装<a name="install"/>
```
sudo apt-get update
sudo apt-get install nginx
```

* 卸载

```
# Removes all but config files.
sudo apt-get remove nginx nginx-common
# Removes everything.
sudo apt-get purge nginx nginx-common 
# After using any of the above commands, use this in order to remove dependencies used by nginx which are no longer required.
sudo apt-get autoremove 

```

***

###3.启动/停止<a name="start_command"/>
```
# service nginx status
# /etc/init.d/nginx status

# /etc/init.d/nginx start
# /etc/init.d/nginx stop

# 启动nginx
systemctl start nginx
# 自启动nginx
systemctl enable nginx
# 查看 nginx 的状态
systemctl status nginx
```

***

###4.查看php配置文件目录<a name="search_directory"/>
```
root@Tim_s_Server2:/etc/init.d# find / -name 'php.ini'
/etc/php/7.0/fpm/php.ini
/etc/php/7.0/cli/php.ini

root@Tim_s_Server2:/etc/init.d# php -i | grep php.ini 
Configuration File (php.ini) Path => /etc/php/7.0/cli
Loaded Configuration File => /etc/php/7.0/cli/php.ini
```
***

###7.配置Nginx至支持PHP<a name="support_php"/>
>https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-debian-8

```
# vi /etc/nginx/sites-available/default
```

```
	# Add index.php to the list if you are using PHP
	index index.php index.html index.htm index.nginx-debian.html;

	server_name _;

	location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
		try_files $uri $uri/ =404;
	}

	# pass PHP scripts to FastCGI server
	#
	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
	#
	#	# With php-fpm (or other unix sockets):
		fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
	#	# With php-cgi (or other tcp sockets):
	#	fastcgi_pass 127.0.0.1:9000;
	}

	# deny access to .htaccess files, if Apache's document root
	# concurs with nginx's one
	#
	location ~ /\.ht {
		deny all;
	}
```

* 1.测试配置是否成功

```
root@glb-gz-debian:/var/www/html# touch info.php
root@glb-gz-debian:/var/www/html# vi info.php

#把这写入 info.php
<?php
  phpinfo();
?>
```


***

###9.更改 nginx 的默认 www 路径.<a name="change_default_directory"/>
>https://www.digitalocean.com/community/tutorials/how-to-move-an-nginx-web-root-to-a-new-location-on-ubuntu-16-04

* 1.移动项目的文件到指定的地方
```
$ rsync -av /var/www/html /home/tian/www
```
* 2.Updating the Configuration Files
```
$ vi  /etc/nginx/sites-enabled/default
```
```
  # include snippets/snakeoil.conf;
       #root /mnt/volume-nyc1-01/html;
	root /home/tian/www/html

       # Add index.php to the list if you are using PHP
```
* 3.Restarting Nginx
```
#测试配置文件是否正常
$nginx -t
$systemctl restart nginx
#删除旧的目录文件
$rm -Rf /var/www/html
```






