#speedtest-cli测速工具

#####服务器网络测试工具.

>安装: https://www.howtoforge.com/tutorial/check-internet-speed-with-speedtest-cli-on-ubuntu/


### [1.用法](#usage)
###[2.安装](#install)
###[4.外网速度测试,到长沙(6132)](#out_net)
### [5.安装了 bbr 后](#after_install_bbr)


***
***
***




### 1.用法<a name="usage"/>
* 1.http://www.ttlsa.com/linux/use-speedtest-cli-test-internet-speed/
* 2.https://fiveyellowmice.com/posts/2016/12/bbr-congestion-algorithm-dark-science.html

***


***
###3.安装<a name="install"/>
* 1.这次用的是第二种的方法去安装 speedtest-cli

```
root@Tim_s_Server2:~# cd /tmp
root@Tim_s_Server2:/tmp# wget https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py
--2017-11-09 02:37:53--  https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 151.101.72.133
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|151.101.72.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 47441 (46K) [text/plain]
Saving to: 'speedtest.py'

speedtest.py                  100%[==============================================>]  46.33K  --.-KB/s    in 0.003s  

2017-11-09 02:37:54 (13.0 MB/s) - 'speedtest.py' saved [47441/47441]

root@Tim_s_Server2:/tmp# ls
speedtest.py
root@Tim_s_Server2:/tmp# chmod 755 speedtest.py
root@Tim_s_Server2:/tmp# mv speedtest.py /usr/local/bin/speedtest-cli
root@Tim_s_Server2:/tmp# speedtest-cli
Retrieving speedtest.net configuration...
Testing from Choopa, LLC (45.77.16.218)...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Hosted by h3zjp (Nerima) [19.05 km]: 21.839 ms
Testing download speed................................................................................
Download: 37.18 Mbit/s
Testing upload speed................................................................................................
Upload: 98.50 Mbit/s

```

***

###4.外网速度测试,到长沙(6132)<a name="out_net"/>
> speedtest-cli --bytes --server=6132 --share

```
root@Tim_s_Server2:/tmp# speedtest-cli --bytes --server=6132 --share
Retrieving speedtest.net configuration...
Testing from Choopa, LLC (45.77.16.218)...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Hosted by ChinaTelecom.Hunan (Changsha) [2648.26 km]: 123.793 ms
Testing download speed................................................................................
Download: 0.26 Mbyte/s
Testing upload speed................................................................................................
Upload: 0.29 Mbyte/s
Share results: http://www.speedtest.net/result/6777708741.png
```
![](/assets/6777708741.png)

***

### 5.安装了 bbr 后<a name="after_install_bbr"/>
>20171109,11:00

```
root@Tim_s_Server2:/tmp# speedtest-cli --bytes --server=6132 --share
Retrieving speedtest.net configuration...
Testing from Choopa, LLC (45.77.16.218)...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Hosted by ChinaTelecom.Hunan (Changsha) [2648.26 km]: 184.77 ms
Testing download speed................................................................................
Download: 0.47 Mbyte/s
Testing upload speed................................................................................................
Upload: 0.50 Mbyte/s
Share results: http://www.speedtest.net/result/6777716969.png
```
![](/assets/6777716969.png)


