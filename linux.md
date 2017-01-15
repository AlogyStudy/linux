linux相关命令操作

* 查看当前目录的文件信息
```
> ls  // list
> ls 目录  // 查看指定目录的文件信息
```

* 目录切换
```
> cd 目录地址
```
 
* 显示当前用户所在位置
```
> pwd
```

* 查看当前用户信息
```
> whoami
```

* 切换用户
```
> su - root // 切换为root管理员用户
> su - // 切换为root 管理员用户
> su root // 切换为root管理员用户（权限还是普通用户）

> exit // 从root用户切换为普通用户 // 从root 直接执行exit表示退出
> su 具体用户 // 切换为指定用户
```
 
* 操作模式切换
```
> init 3 // 桌面模式切换为命令模式
> init 5 // 命令模式切换为桌面模式
```

* 显示系统分区
```
> df -lh 
```

* 创建普通用户
```
> useradd
```

* 查看文件指定大小
```
> du -h filename
```



# 系统常用指令

> 信息匹配

```
> grep 关键字 路径名 // 将文本中指定的信息匹配出来
> grep own ./newpasswd 
> grep own /etc/passwd 
```

> 查看进程

任务管理器，查看系统进程及所占资源
```
> top 
```
退出进程`q`


> 查看活跃进程

```
> ps // 查看系统活跃进程process
> ps -A // 查看所有进程
```

> 查看内存使用情况

```
> free
> free -m  // 查看内存情况
```

> 显示文件占据磁盘大小

```
> du -h filenname // 以K，M，G为单位显示或文件占据磁盘空间大小（硬盘中最小的`block`是4k）
```
    
> 时间

```
> date // 查看系统时间
> date -s "2017-1-15 16:06:06" //  给系统设置时间
```    
 
> 查看系统分区

```
> df -lh // 查看系统分区信息
```    
 
> 杀死进程

```
> kill -9 pid // 杀死指定进程号的进程
> kill -9 1922
```    

# 管道

管道（pipe）：前者的输出是后者的输入

```
> ls -al | wc // 查看当前目录下一共的文件数目
> ls -al | grep 关键词 
> ls -al | head -10 
> cat newpasswd | grep 'nologin'
> ls -al | less | head -10
``` 

递归使用管道
```
> ls -al | grep mm | wc // 查看当前目录下有多少文件。
```

# 文件查找

`find`文件查找

```
> find 目录 参数 参数值, 参数 参数值, 参数 参数值...
 
> find / -name  passwd // 查询名字
> find /etc -name passwd
> find / -maxdepth 3 -name passwd // 指定查询文件层次
> find / -mindepth 3 -maxdepth 3 -name passwd 
``` 

参数：
* -maxdepth n 查找目录最深层次
* -mindepth n 查找目录最浅层次
* -name filename 根据文件名称
* -size 大小 根据文件大小进行查找 (大小单位默认：512字节[半k]) 
```
> find  ./ -size 10c // 修改单位 （1c=1字节）
> find  ./ -size 10k // 修改单位 
> find ./ -size +5000c // 大于指定值
> find ./ -size -10c // 小于指定值
```
* -perm 根据权限查找
```
> find ./ -perm  666
```
* -type f/d 根据文件还是目录查找
```
> find ./ -maxdepth 1 -type d // 查找当前一级目录
```
* -user -uid -nouser 当前用户
* -group -gid -nogroup 当前组