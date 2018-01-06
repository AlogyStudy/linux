
## 认证

资源分派（资源的合理分配）:
- `Authentication`: 认证
- `Authorization`: 授权
- `Accounting`: 审计
 

认证机制： 用户和组
`token`机制：只有密码，而没有用户名
`identity`机制：每个用户都有`username`，`password`


Linux用户：`Username/UID`
- 管理员：root/0
- 普通用户: 1-65535，系统用户：1-499(守护进程获取资源进行权限分配)，登录用户: 500+ (交互式登录)


Linux组：`GroupName/GID`
- 管理员组：root/0
- 普通组：系统：1-499，普通组：500+

有些概念中，组等同于角色

Linux安全上下文：

计算机的操作是直接指挥计算机？
当想完成一个事情的时候，只能发起一个程序。计算机完成工作靠的是程序的运行。
运行中的进程：进程（process）

安全上下文：以进程发起者的身份运行

进程所能够访问的所有资源权限取决于进程的发起者的身份


Linux组的类别：
- 用户的基本组(主组)：组名同用户名，且仅包含一个用户叫做私有组
- 用户的附加组

## 用户和组相关的配置文件

Linux用户和组相关的配置文件：
- /etc/passwd：用户及其属性信息（名称，UID，基本组ID...）
- /etc/group：组及其属性信息
- /etc/shadow：用户密码及其相关属性
- /etc/gshadow：组密码及其相关属性


`/etc/passwd`:
`account:password:UID:GID:GECOS:directory:shell`
用户名:密码占位符:UID:GID:GECOS(用户完整信息，用户全名，家庭电话，办公电话...):主目录:默认shell


`/etc/group`:
`group_name:passwd:GID:user_list`
组名:组密码占位符:GID:以当前组为附加组的用户列表(分隔符逗号隔开)

`/etc/shadow`:
用户名:加密后密码:最近一次更改密码的日期:密码的最小使用期限:最大密码使用期限:密码警告时间段:密码禁用期:账户过期日期:保留字段

加密机制：单向加密（提取数据指纹）
`md5: message digst, 128bits`
`sha1：secure hash algorithm, 160bits`
`sha224: secure hash algorithm, 224bits`

雪崩效应：初始的条件的微笑改变，将会引起结果的巨大改变。
定长输出

密码的复杂性策略：

- 使用数字，大写字母，小写字母及特殊字符中至少3种
- 足够长
- 不要易猜测，使用随机密码
- 定期更换



## 用户和组相关的管理命令

用户和组相关的管理命令

> useradd

用户创建: `useradd`
`account:password:UID:GID:GECOS:directory:shell`

```
useradd [option] user_name
-u UID, [UID_MIN, UID_MAX]定义在`etc/login.defs`
-g GID:指明用户所属基本组，可谓组名，也可以GID
-c "COMMENT",用户的注释信息
-d /PATH/TO/HOME_DIR: 以指定的路径为家目录
-s SHELL:知名用户的shell程序，可用列表在/etc/shells文件中
-G GID：为用户指明附加组，组必须事先存在
-r 创建系统用户
````

```
id root // 查询用户相关ID信息
```

> groupadd

```
groupadd [option] group_name

-g GID: 指明IGD号：[GID_MIN, GID_MAX]定义在`etc/login.defs`
```

`su`:切换用户或以其他用户身份执行命令
```
su [options] [-] [args]
```
切换用户的方式：
```
su UserName: 非登录式切换,即不会读取目标用户端配置文件
su - UserName: 登录式，会读取目标用户配置文件，完全切换
```

换个身份执行命令：
```
su [-] UserName -c 'COMMAND'
```

## 用户属性相关

`usermod`: 修改一个用户基本属性
```
usermod [OPTION] login
usermod  -a -G list user7

userod -d /home/newUser6 -m user6

-u UID: 新UID
-g GID: 新的基本组
-G GROUP1， 新的附加组，原来的附加组将会被覆盖，若保留原有，则要同时使用-a选项，表示append
-s SHELL: 新的默认SHELL
-c 'COMMENT': 新的注释信息
-d HOME: 新的家目录，原有家目录中的文件不会同时移动至新的家目录。若要移动，同时使用-m选项
-l login_name: 新的名字

-L lock指定用户
-U unlock指定用户

-e YYY-MM-DD: 指明用户帐号过期日期
-f INACTIVE:设定非活动期限
```

> 用户添加密码

`passwd UserName`：修改指定用户的密码，仅root用户可以
`passwd`：修改用户密码

常用选项：
```
-l: 锁定指定用户
-u: 解锁指定用户

-n mindays: 指定最短使用期限
-x maxdays: 最大使用期限
-w warndays: 提前多少天开始警告
-i inactivedays: 非活动期限

--stdin：从标准输入接受用户密码
echo "PASSWORD" | passwd --stdin USERNAME
echo 'centos' | passwd --stdin user1 &> /dev/null
echo $?
```

`/dev/null`: `bit buckets`，吞噬任何数据
`/dev/zero`: 吐0数据，要多少有多少数据


> 删除用户

`userdel [OPTION] login`:
```
-r: 删除用户家目录
```

> 组属性修改

`groupmod [OPTION] group`:
```
groupmod GROUP
-n grup_name: 新名字
-g GID：新的GID
```

> 删除组

`groupdel`
```
groupdel GROUPD
```

> 组密码

`gpasswd`

```
gpasswd user

-a user: 将user添加至指定组中
-d user：删除用户user的以当前组为组名的附加组

-A user1,user2： 设置有用户管理权限的用户列表
```


`newgrp`: 临时切换基本组
`pwck`: 检查密码文件的完整性


> 修改用户的信息

`chage`: 更改用户密码过期信息
 
