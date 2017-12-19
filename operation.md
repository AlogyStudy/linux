
## other

初级：系统基础
中级：系统管理、服务安全及服务管理、Shell脚本
高级：
MySQL数据库：
	cache & storage
集群：
	Cluster
	
	lb:// 负载均衡集群
		4layer
		7layer
	hb:// 高可用集群
分布式：
	zookeeper
	分布式文件系统
虚拟化技术：
	xen
	kvm
Openstack: 
	IAAS云

运维工具：
	ansible
	puppet(ruby), saltstack(python)
监控工具：
	zabbix
大数据处理：
	hadoop
	spark, storm

	elk: elastcsearch, logstash, kibana
docker
	
Python

## OS

现代计算机设备的组成部分：
运算器，控制器，存储器，输入设备，输出设备
	CPU
	bus: 总线
	memory: 编址存储单元

	read ahead

IO: 与外部部件交互
	磁盘
	网卡

虚拟机：虚拟计算机
	软件 + 硬件 模拟出的虚拟设备
	
CPU: 运算器和控制器组成。
	一个CPU，就是一个芯片。	

CPU指令，指令集：
- 特权指令：OS运行特权指令
- 普通指令：应用程序语言只能调用普通指令

接近于人类阅读的语言称之为高级语言，接近于机器的称之于低级语言。
	
高级语言 -> 汇编语言（装换为芯片支持的汇编语言） -> 对机器指令的调用

> OS

OS: Operating System

- 软件程序
- 通用目的
	硬件驱动，进程管理，内存管理， 网络管理， 安全管理

System Call(Syscall)，系统调用: 应用程序向系统内核申请执行特权指令。

编程层次：
	硬件规格：hardware specification
	系统调用：
	库调用：library call，把非常多的底层功能，整合出来，提供离最终目标更近的功能。

	kernel -> lib/系统调用 -> OS

程序启动：
- 开机自动启动
- 人为启动，完成人为启动，需要有一个程序允许与计算机打交道。这个程序称之为：用户接口（UI/前端）

UI：
	GUI：Graphic User Interface 图形用户接口/图形用户界面
	GLI: Command Line Interface 命令行用户接口

在众多的接口中，有一类特殊的接口为，用户接口。
用户通过用户接口来指挥其它程序的运行。

ABI：Application Binary Interface 运行程序接口，接口格式/规范
API: Application Programming Interface 应用编程接口


CPU架构类型：

- x86 （intel）
- x64 （intel）
- arm （高通）
- m68000 -> m68k（摩托罗拉）
- power，第一个多核CPU，第一个4GHz（IBM）
- ulterasparc （Sum）
- alpha （惠普）
- 安腾


每一种CPU提供的指令集个不一样，无论怎么编译，如果只支持x86类型的，是无法运行起来。


## 操作系统

```
Windows
Linux:
	Linus --> Linux

	GNU/Linux
Unix： 
	System：AIX（IBM），Solaris（SUM）,HP-UX（HP）
	BSD：Berkeley System Distribution: NetBSD, OpenBSD, FreeBSD


MIT：
	GNU： GNU is Not Unix
	GPL：General Public License
```

计算机的基础知识：
CPU（运算器+控制器），memory，I/O（输入设置+输出设备）

程序运行模式：
	用户空间：user space, US
	内核空间：system space

运行程序格式：
	Windows: ExE, 库文件dll(dynamic link  blirary)
	Linux: ELF, 库文件so	(shared object)

程序：指令 + 数据
	指令：只读
	数据：读写
程序：算法 + 数据结构

库调用，系统调用：从本质上讲都是别人写好的程序，可以直接拿来使用。// malloc()申请内存, free()释放内存

编程语言：
- 汇编语言：维码编程(系统中与硬件相关的特有代码，驱动程序开发)
- 高级语言C,C++：系统级应用
- 高级应用java，python，php：应用程序

```
kenrel, glibc, bash --> 编译成对应的执行文件，组成系统
```

## Linux发行版

主流发行版本：
```
slackware:
	suse // 二次发行版本
		opensuse // (基于sure发行的) // 三次发行版本
		sles
debian:
	ubuntu // 二次发行版本
		mint  // 三次发行版本
redhat:
	rhel: redhat enterprise linux
	CentOS: 兼容rhel的格式 // 在后期被rhel收购，rhel维护二个分支.
	fedora
ArchLinux: 完全独立，轻量，轻巧的程序独立包
Gentoo
LFS：Linux From scratch

Android: kernel + busybox + java虚拟机
```

程序包管理器:

- rpm: RHEL, Fedora, S.u.S.E, CentOS
- dpt: Debian, Ubuntu


CentOS和Linux关系?
CentOS和RHEL是什么关系?
各种开源协议的具体细节：GPL, LGPL, Apache, BSD

> 自由软件

- 自由使用
- 自由学习和修改
- 自由分发
- 自由创建衍生版

> Linux的哲学思想

1. 一切皆文件：把几乎所有的资源，包括硬件设备都组织为文件格式.
2. 由众多单一目的的小程序组成，一个程序只实现一个功能，而且要做好。
3. 尽量避免跟用户交互。目标：实现脚本编程，以自动完成某些功能.
4. 使用纯文本文件保存配置信息。目标：一款使用的文本编辑器即能完成系统配置工作。

获取CentOS的发行版：

(aliyun镜像)[http://mirrors.aliyun.com]
(sohu镜像)[http://mirrors.sohu.com]
(163镜像)[http://mirrors.163.com]

```
startx & // 开启桌面模式
```
-----

```
application
		↑
  library
		↑
 kernel （系统调用：操作系统将硬件抽象出来）
		↑
 hardware（硬件）
```

> 终端

服务器只有网线和电源线，并没有键盘，鼠标，显示器之类的输出设备，不妨碍向外面提供服务。为了系统能够执行配置，可以远程连接，必须需要有一个交互式接口，这个接口程序可能在vda输出，也有可能远程输出到远程终端上。

用户与主机交互，必然要用到设备，称之为：终端设备


大型主机上有一个分屏器，分屏器中的端口或者端子可以接入一个键盘和显示器。
用户键盘+显示器：终端

终端的多种类型：

- 物理终端：本机接入本机的显示器，键盘设备。（从一定程度上讲物理终端也称之为控制台console）设备文件路径：`/dev/console`
- 虚拟终端：附加在物理终端之上的以软件方式虚拟的终端。CentOS默认有6个虚拟终端，使用快捷键`Ctrl + Alt + F1~F6`。设备文件路径：`/dev/tty1~6`
- 图形终端：附加在物理终端之上的以软件方式实现的终端，额外会提供桌面环境（图形终端也是虚拟终端的一种）。
- 模拟终端：图形界面下打开的命令行接口，基于`ssh`协议或`telnet`协议等远程打开的界面。设备文件路径：`/dev/pts/# [0,∞)`

一般来讲系统启动之后，默认使用虚拟终端1登录，而不会使用物理终端，即便在屋里设备上。
刚开机的时候，程序还未运行起来，所有的信息需要输出，这个时候映射的是物理终端，一旦程序启动完成了，默认使用`虚拟终端1`进行用户登录界面。如果默认启动的是图形界面，也会启动`图形终端`。

查看当前的终端设备命令：`tty`
```
/dev/pts/l // 模拟终端
/dev/pts/0 // 图形终端
/dev/tty2 // 虚拟终端2
```

交互式接口：启动终端后，在终端设备附加一个交互式应用程序。
```
GUI: 图形交互程序，会使用到窗口管理器`X protocol -> window manager, desktap`
	Desktap: GNOME(C, 图形开发库：gtk)，KDE(C++, 图形开发库：qt)，XFCE（轻量级桌面）
CLI: 文本界面
	shell程序:
		sh (bourn)
		csh (C语言类似的shell程序)
		tcsh (csh升级版)
		ksh (korn开发的)
		bash (bourn again shell, 开源组织综合其它sh优点开发的shell),遵循GPL协议
		zsh (功能更加强大)
```

显示当前使用`shell`：
```
echo $SHELL
```
显示当前系统使用所有的`shell`
```
cat /etc/shells
```

> 命令

命令提示符：`prompt`
```
[root@localhost ~]#
[admin@localhost ~]$


echo $PS1
	[admin@localhost ~]
	[\u@\h \W]\$

prompt:
管理员：#
普通用户：$
```

命令：
输入命令，回车：提请shell程序找到键入命令所对应的可执行程序或代码，并由分析后提交给内核分配资源将其运行起来，表现为一个或多个进程（运行中的程序称之为进程）。

在`shell`中可执行的命令有两类：
- 内建命令：由`shell`自带的，而且通过某命令形式提供
- 外部命令：在当前系统的某文件系统路径下有对应的可执行程序文件

查找某个外部命令
```
which ls
whereis ls
```

区别外部或内部命令：
```
type cd
```

![](./_image/2017-12-17-22-21-58.jpg)

运行命令：
命令格式，`COMMAND [OPTIONS...] [ARGUMENTS...]`
选项：用户启用或关闭命令的某个或某些功能。短选项：`-c`,例如：`-l, -h,`(大多数情况下多个短选项可合写) 长选项：`--word`,例如:`--long`,`--human-readable`

参数：命令的作用对象。向命令提供数据，

多个选项，多个参数之间都应该要空格隔开。

取消命令执行：`Ctrl + C`


> 文件系统

一个定位系统，需要有一个起始位置

`Linux`是倒置树文件系统

文件数据:
- 元数据：metadata
- 数据：data


`Linux`文件系统特点：
- 文件名严格区分字符大小写
- 文件名可以使用除了`/`以外的任意字符(不建议使用特殊字符)：`/根目录`，`路径分隔符`
- 文件名长度最长不能超过255个字符串
- 所有`.`开头的文件，都是隐藏文件
 directory

路径：
- 绝对路径：从根目录起始的路径
- 相对路径：对当位置其实的路径。当前目录(current)/工作目录(working directory)

```
>pwd  // printing working directory
```

LSB: Linux Standard Base （linxu定义），规定了linux基本的规范。

## 命令

> Linux命令帮助的获取

外部命令：都有一个可执行程序，位于文件系统某目录下。

`shell`程序搜寻可执行程序文件的路径定义在`PATH`环境变量中。
```
echo $PATH
// 自左至右顺序寻找
/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/admin/bin
```

内部命令获取帮助：`help COMMAND`
外部命令：
- `COMMAND --help`
- `COMMAND -h`
- 使用手册`manual`,`man COMMAND`
- 信息页`info COMMAND`
- 程序自身的帮助文档`README`,`INSTALL`,`ChangeLog`
- 程序官方文档：官方站点`Documentation`
- 发行版的官方文档
- Google

```
> hash
```

shell搜寻到的外部命令的路径结果会缓存至kv(key-value)存储中。
输入的命令第一次会在各自可执行程序文件中寻找，然后存储在缓存中（可理解为内存中的一段空间），后续使用中，从缓存中查找。


```
> history
> history -a // 手动追加本次会话新执行的命令历史列表至历史文件中
> history -c // 清空命令历史
```
管理命令历史
登录系统之后，输入的每一个命令都记录在历史记录缓冲当中，一旦登出（`exit`,`logout`）之后会放置在历史文件`.bash_history`中。
登录`shell`时，会读取命令历史文件中记录下的命令:`~/.bash_shitory`


快捷操作:
```
> !# // !7 // 调用历史记录中第#条命令
> !string // !man // 调用历史记录中最近一个以string开头的命令
> !! // 重复运行上一条命令
```

CentOS系统中，手册页:`/usr/share/man`
`man1 ... man8`
系统之上有很多命令，有些命令出于管理的目的，有点普通用法目的。不同目的，不同权限的的命令，一般是分门别类进行存放。
```
> man COMMAND
> man read
> man 2 read // 查看指定章节的帮助手册
> whatis COMMAND
> whatis read // 查看那些章节下有相关文档
```
- man1: 用户命令
- man2: 系统调用
- man3: C库调用(系统库)
- man4: 设备文件（`/dev`底下的文件）及特殊文件
- man5: 配置文件格式
- man6: 游戏
- man7: 杂项
- man8: 管理类的命令

`man`命令的配置文件：`/etc/man.config`
`MANPATH`变量定义`man`命令到哪边搜索文件路径

```
nano /ect/man.confg // 编辑器
```
