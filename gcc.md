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







