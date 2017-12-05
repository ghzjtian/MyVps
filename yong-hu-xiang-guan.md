#用户相关
>http://www.cnblogs.com/daizhuacai/archive/2013/01/17/2865132.html


###1.添加用户

* 1.没有主目录的创建
```
root@Tim_s_Server2:~# useradd webAdmin
root@Tim_s_Server2:~# passwd webAdmin
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
```

* 2.有主目录的创建
```
root@Tim_s_Server2:/home/tian/www# useradd -d /home/webAdmin2 -m webAdmin2
root@Tim_s_Server2:/home/tian/www# passwd webAdmin2
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
```


###2.用户的 sudo 授权



###3.web项目管理组
