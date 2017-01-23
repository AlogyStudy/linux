
# gcc编译器

安装gcc：
```
gcc-4.4.7-4.el6.i686.rpm
gcc-c++-4.4.7-4.el6.i686.rpm
```
需要安装依赖.
```
error: Failed dependencies:
	cloog-ppl >= 0.15 is needed by gcc-4.4.7-4.el6.i686
	cpp = 4.4.7-4.el6 is needed by gcc-4.4.7-4.el6.i686
	glibc-devel >= 2.2.90-12 is needed by gcc-4.4.7-4.el6.i686
	libgomp = 4.4.7-4.el6 is needed by gcc-4.4.7-4.el6.i686
	libgomp.so.1 is needed by gcc-4.4.7-4.el6.i686
```

A软件依赖B软件，B软件依赖C软件，C软件依赖D软件。
A软件安装的时候，需要B，C，D软件的支持。 先安装D，安装C，安装B，安装A。
卸载C软件的时候，需要先卸载B软件。卸载B软件会提示先卸载A软件。 卸载A，卸载B，卸载C

测试gcc安装是否成功：
```
#include <stdio.h>
main() {
    printf('hello world\n');
}
```
编译：
```
> gcc filename
```


# zlib

软件解压缩
后缀:`tar.gz` --> `tar zxvf 压缩包` 
后缀：`tar.bz2` -->  `tar jxvf 压缩包`

```
> tar zxvf 压缩包名字
```

安装zlib软件(源码配置方式安装)
* 检查配置软件的依赖关系 configure
```
检查软件依赖关系
设置软件安装路径
软件参数配置
```
configure指令,作为配置.
```
> ./configure --help
> ./configure --prefix // 设置软件安装目录
```
`zlib`软件安装的时候做配置`configure`,不需要设置额外的参数，系统会把其它安装在默认的目录，以便其它软件可以找寻其配置 。

检查配置
```
> ./configure
```

* 编译软件 make
例如：把c语言的二进制文件编译成可执行 二进制代码。
```
> make
```
* 安装软件 make install
把编译后的二进制文件复制到系统指定目录
```
> make install 
```

安装软件三步：
1. 检查配置:`./configure`
2. 编译软件: `make`
3. 安装软件: `make install`

# apache编译安装

安装顺序：
`apache` -> `php` -> `mysql`


> 解压文件

```
> ./configure --prefix=/usr/local/http2 \  
> --enable-modules=all \ 
> --enable-mods-shared=all \ 
> --enable-so
```
apache软件里边有许多功能模块modules，与软件本身是两部分内容,`--enable-mods-shared=all`，参数作用是把modules模块的代码也编译进软件的本身里边。缺点：本身物理体积变大，优点:运行速度快.
不把模块编译进软件内，这样软件体积可以小巧，如果需要那个模块就立刻`include`进来使用.

> 编译和安装
```
> mask && mask install
```

> 启动apache

```
> /usr/local/http2/bin/apachectl start 
```

> 通过setup指令开放防火墙的80端口



> 通过浏览器请求apache服务


## apache配置虚拟主机

打开`httpd.conf`
```
打开httpd-vhosts.conf辅助配置文件
```

修改配置`httpd-vhost.conf`文件
```
<VirtualHost *:80>
	DocumentRoot "/home/mm/1111"
	Servername local.com
</VirtualHost>
```

重启apache `./apachectl restart`

windows下的host文件需要配置dns域名解析
```
192.167.1.10 local.com
```

> 访问权限问题

提示：`Forbidden`

* 开启apache配置文件的目录访问权限
```
<Directory/>
	Options FollowSymLinks
	AllowOverride Node
	Order deny,allow
	Allow from all
</Directory>
```

* 没有默认索引文件

```
> touch /home/mm/1111/index.html
```

* 文件目录权限

文件的执行权限必须要有。


# 安装PHP

php有许多依赖包程序：`libxml`，`gd`，`jpeg`，`png`等等.

> 解压文件



> 安装libxml2

```
shell> cd /home/shuhua/tar
shell> tar zxvf libxml2-2.7.2.tar.gz 
shell> cd libxml2-2.7.2
shell>./configure --prefix=/usr/local/libxml2 
shell> make && make install
```

> 安装jpeg8

```
shell> cd /home/shuhua/tar
shell> tar -zxvf jpegsrc.v8b.tar.gz 
shell> cd jpeg-8b 
shell>./configure --prefix=/usr/local/jpeg \
--enable-shared --enable-static 
shell> make && make install
```

> 安装libpng

```
shell> cd /home/shuhua/tar
shell> tar zxvf libpng-1.4.3.tar.gz 
shell> cd libpng-1.4.3 
shell>./configure  # 不要带参数，让它默认安装到相应目录
shell> make && make install
```

> 安装freetype

```
shell> cd /home/shuhua/tar
shell> tar zxvf freetype-2.4.1.tar.gz 
shell> cd freetype-2.4.1
shell>./configure --prefix=/usr/local/freetype 
shell> make && make install
```

> 安装GD库

```
shell> cd /home/shuhua/tar
shell> tar -zvxf gd-2.0.35.tar.gz 
shell> mkdir -p /usr/local/gd 
shell> cd gd-2.0.35 
shell>./configure --prefix=/usr/local/gd  \
			--with-jpeg=/usr/local/jpeg/ 	\
			--with-png --with-zlib \
			--with-freetype=/usr/local/freetype
shell> make && make install
```

> 安装PHP
```
shell> cd /home/shuhua/tar
shell> tar -jxvf php-5.3.6.tar.bz
shell> cd php-5.3.6
shell>./configure --prefix=/usr/local/php \
--with-apxs2=/usr/local/http2/bin/apxs \   //  对apache的支持。 与apache结合使用，在httpd.conf里面会自动引入PHP模块，也会自动创建对应的apache，php模块
--with-mysql=mysqlnd \     // 数据库支持 mysql native driver
--with-pdo-mysql=mysqlnd \
--with-mysqli=mysqlnd \
--with-freetype-dir=/usr/local/freetype \
--with-gd=/usr/local/gd \
--with-zlib --with-libxml-dir=/usr/local/libxml2 \
--with-jpeg-dir=/usr/local/jpeg \
--with-png-dir \
--enable-mbstring=all \   //  宽字节函数库支持(mb_substr())
--enable-mbregex \      // PHP中的表达式支持
--enable-shared      // PHP的函数库编译到本身软件中

shell> make && make install 
shell> cp php.ini-development /usr/local/php/lib/php.ini   // 复制`php.ini-development` 系统指定目录。
```

注意点：
软件安装失败，需要重新安装：
1. 直接删除对应的程序文件。例如：/usr/local/http2. 删除`http2`目录。
2. 删除解压后的文件。
3. 重新解压，重新配置configure，重新编译make，重新安装make install


配置Apache使其支持PHP

修改配置文件`httpd.conf`
```
> vi /usr/loca/http2/conf/httpd.conf
```
* 在httpd.conf（Apache主配置文件）中增加：
```
AddType application/x-httpd-php .php
```
* 找到下面代码
```
<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>
```
在index.html前面`index.php`
* 建立php测试网页
```

> vi /home/mm/index.php
```
输出内容：
```
<?php
    phpinfo();
?>
```

* 重启apache
```
> /usr/local/http2/bin/apchectl restart
```

* 访问到浏览器`http://虚拟机IP`

看到PHP信息，完成。

注意：
PHP模块安装后重启apache如果提示语法错误，`Syntax error on line on 105 of `
作用：告知系统创建了一个PHP模块.
解决办法：
```
> echo '/usr/local/lib' >> /ect/ld.so.conf
> ldconfig
```
让系统重新识别模块信息


# 安装Mysql

> 编译安装Mysql

```
shell> cd /home/shuhua/tar
shell> tar -xzvf mysql-5.1.58.tar.gz
shell> cd mysql-5.1.58	
shell> ./configure --prefix=/usr/local/mysql \	
		--with-charset=utf8 \ 		   // mysql 对字符集的支持	
		--with-extra-charsets=gbk,gb2312,binary	    //  mysql额外字符集支持
shell> mount // .....挂载光盘 安装依赖.
shell> rpm -ivh libtermcap-devel-2.0.8-46....
shell> make && make install
```


> 配置并初始化MySQL

```
shell> groupadd mysql	
shell> useradd  -g mysql mysql	
shell> cp support-files/my-medium.cnf /etc/my.cnf  // mysql配置文件拷贝系统指定目录,并修改文件名 
shell> cd /usr/local/mysql
shell> chown -R mysql.mysql . // 递归修改组和文件的主人 为当前目录`.`
shell> bin/mysql_install_db --user=mysql \
--datadir=/usr/local/mysql/var
// 创建mysql测试数据库和系统的数据库。 把数据存放到var目录下. (在mysql的bin目录下执行)
shell> chown -R root .	
		// 把当前目录文件的主人都改为root，避免数据库恢复为出厂设置。 (在mysql的bin目录下执行)
shell> chown -R mysql var 
shell> bin/mysqld_safe --user=mysql &	
		// 启动mysql，`&`表示在后台运行mysql服务
```

搜寻进程
```
> ps -A | grep 'mysql'
```

登陆mysql
```
> ./mysql // 在bin目录
```

设置密码：
通过数据表的形式修改密码
```
> use mysql
> desc user

> seelct User,Password,Host from user

> update user set Password=password(Pass1234)   // 设置密码并加密
```

刷新mysql权限,(无论是设置密码，还是增减权限都需要刷新mysql权限)，是密码生效
```
> flush privileges
```


注意：
* 安装完之后，gnome已经奔溃，不要使用桌面模式.
```
> cd /etc
> vi inittab
```

* apache 和 mysql  启动方式不同
设置系统自动启动

配置文件路径：
在 `/etc/rc.d/rc.local` 文件中增加启动apache的命令
```
/usr/local/http2/bin/apachectl start 
/usr/local/mysql/bin/mysqld_safe --user=mysql &
```
-----
```
> vi /etc/rc.d/rc.local
```

系统重启
```
reboot
```

关机
```
poweroff
```

