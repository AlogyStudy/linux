
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


