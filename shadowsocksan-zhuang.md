#shadowsocks安装

>https://github.com/shadowsocks/shadowsocks-libev#debian--ubuntu

###1、追加软件源
>debian 9

1.查看系统版本
```
root@Tim_s_Server2:~# lsb_release -a
No LSB modules are available.
Distributor ID:	Debian
Description:	Debian GNU/Linux 9.1 (stretch)
Release:	9.1
Codename:	stretch
```

```
echo "deb http://shadowsocks.org/debian stretch main" >> /etc/apt/sources.list
```


###2.然后更新源并安装


~~apt-get update
apt-get install shadowsocks~~


For Debian 9 (Stretch)
```
sudo sh -c 'printf "deb http://deb.debian.org/debian stretch-backports main" > /etc/apt/sources.list.d/stretch-backports.list'
sudo apt update
sudo apt -t stretch-backports install shadowsocks-libev
```


###3.配置 shadowsocks 文件
```
root@Tim_s_Server2:~# cat /etc/shadowsocks/config.json
{
    "server":"1.1.1.1",
    "server_port":8388,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"111111",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false,
    "workers": 1,
    "prefer_ipv6": false
}

```


###4、重启shadowsocks服务
```
/etc/init.d/shadowsocks status
/etc/init.d/shadowsocks stop
/etc/init.d/shadowsocks start
```

###5.MyJapan Server ss二维码





