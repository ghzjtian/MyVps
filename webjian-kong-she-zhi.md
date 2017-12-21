#Web监控设置
>服务器自动监控: https://www.zhihu.com/question/21073555

## 1.DataDog

## 2.aliyun 的 云计算基础服务/云监控（已在使用）

***
***
***

## 1.DataDog
>安装教程: https://app.datadoghq.com/signup/agent#debian
>服务器自动监控: https://www.zhihu.com/question/21073555

#### 注意事项:
* 1.安装后可能需要几分钟的时间让后台上报事件.

* 2.VPS 的主机名(hostname)必须要符合 rfc-1123 的格式.
>Hostnames must comply with RFC-1123, which permits only "A" to "Z", "a" to "z", "0" to "9", and the hyphen (-).

* 3.debian系统的基本用法:
>https://docs.datadoghq.com/guides/basic_agent_usage/deb/

* 4.加入 TCP/HTTP 的检查(在 /etc/dd-agent/conf.d 文件夹中).
>https://app.datadoghq.com/monitors#create/network
    * tcp 实例:
    ![](/assets/ScreenShot2017-12-21_14.35.05.png)
    * http 实例: 
    ![](/assets/ScreenShot2017-12-21_14.47.52.png)
    * 重启后，查看 info 的结果:
    ![](/assets/ScreenShot2017-12-21_14.49.19.png)
    
* 5.Alert 信息接收.
    * 下载 Slack,用来收到报警的信息.(不知怎么操作)
    * 登录的 email 也可以立刻收到报警的信息.(未验证)
    
    
***
    
## 2.aliyun 的 云计算基础服务/云监控（已在使用）.
>https://cloudmonitor.console.aliyun.com/index?spm=5176.128766.653105.2.7oB8hC&custom_trace=2017-02-07&callback=/hostmonitor/host#/home/ecs

***









