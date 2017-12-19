#ssh安装



查看状态:netstat -antulp | grep ssh
启动：/etc/init.d/ssh start 


###1.添加 ssh key(公钥免密登陆)。
* 1.ssh 免密登陆教程: http://www.jianshu.com/p/f5a142cf3936

ssh root@45.77.19.119

 

###2.用scp 上传和下载文件.
* 1.把文件上传到 /tmp,然后再把文件到需要的文件里面
```
scp /Users/tianzeng/.ssh/id_rsa.pub git@10.100.1.217:/tmp
mv /tmp/id_rsa.pub /home/git/.ssh/authorized_keys
```

* 2.文件下载
```
$ scp tian@10.100.1.217:/home/git/hello.txt /Users/tianzeng/Desktop
```