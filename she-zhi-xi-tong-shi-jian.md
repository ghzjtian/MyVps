#设置系统时间
>https://wiki.debian.org/DateTime
>https://www.hugeserver.com/kb/config-time-date-debian-8-ntp/

>使用 NTP 服务器去自动纠正.

***

###* 1.设置自动纠正时间

* 1.更新源.
```
# apt-get update
```
* 2.安装 ntp .
```
# apt-get install ntp
```
* 3.备份 localtime .
```
# mv /etc/localtime /etc/localtime.back
```
* 4.建立链接.
```
# ln -s /usr/share/zoneinfo/PRC /etc/localtime
```
* 5.重启 ntp.

```
#service ntp restart

```

***

###* 2.查看当前的时间
```
root@Tim_s_Server2:/etc# date
Wed Nov 15 13:52:41 CST 2017
```
