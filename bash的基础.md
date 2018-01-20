

## 命令历史

`history`
环境变量：
- `HISTSIZE`: 命令历史记录的条数，`~/.bash_history`

```
history # // 显示历史中最近的#条命令
!#: 重复执行第#条
!!: 上一条命令
!string： 最近一条string命令
```

环境变量：`HISTCONTROL`
ignoredups: 忽略重复的命令，连续且相同为“重复”
ignorespace: 忽略所有以空白开头的命令

修改环境变量值方式：

```
export 变量名 = '变量值' // 当前bash有效
```

## 命令补全

模糊命令 + `tab`

bash执行命令：
- 内部命令
- 外部命令：bash根据PATH环境变量定义的路径，自左而右在每个路径搜寻以给定命令命名的文件，第一次找到即为要执行的命令


## 路径补全

把用户给出的字符串当作路径开头，并在其指定上级目录下搜索以指定的字符串开头的文件名



## 命令行展开

`~`：展开为用户的主目录
`~USERNAME`：展开为指定用户目录
`{}`: 可承载一个以逗号分隔的列表，并将其展开为多个路径
	/tmp/{a, b} = /tmp/a, /tmp/b


## 命令的执行结果状态

成功
失败

`bash`使用特殊变量`$?`保存上一条执行成功或失败的状态结果。

- 0：成功
- 1 - 255: 失败

```
> echo $?
```

程序执行有两类结果：

- 程序的返回值
- 程序的执行状态结果


## 命令别名

`alias`命令别名

显示已有可用别名：
```
alias
```

定义别名：
```
alias [-p] [name[=value] ... ]
alias cdnet='cd /etc/sysconfig/network-scripts/'
```

仅对当前`bash`进程有效

仅对当前用户：`~/.bashrc`
对所有用户有效：`/etc/bashrc`
修改配置文件，在新进程中才能读取，或者当前进程重新读取配置文件
```
source .bashrc
```

撤销别名：
```
unalias -a // 移除所有
unalias name // 移除指定
```



## bash快捷键

```
Ctrl + l：清屏，相当于clear命令

Ctrl + a：跳转至命令开始处
Ctrl + e：跳转至命令结尾处

Ctrl + c：取消命令执行

Ctrl + u：删除命令行首至命令行所在处的所有内容
Ctrl + k：删除命令行尾至命令行所在处的所有内容
```


## bash的I/O重定向

程序：指令 + 数据
	
读入数据：`Input`
输出数据：`Output`

打开的文件都有一个`fd`: `file descriptor`(文件描述符)

标准输入（设备）：`keyborad`， `0`。
标准输出（设备）：`monitor`，`1`
标准错误输出：`moniter`，`2`


`I/O`重定向：改变标准位置

输出重定向：`COMMAND > NET_POS`（覆盖重定向）,`COMMAND >> NEW_POS`(添加重定向)
标准错误输出：`COMMAND 2> NET_POS`（覆盖重定向错误输出数据流），`COMMAND 2>> NET_POS`（添加重定向错误输出数据流）

```
ls /var/ > /tmp/etc.out

set -C：禁止将内容覆盖输出已有文件 // 对当前bash有效
set +C：打开将内容覆盖输出已有文件 // 对当前bash有效
```

标准输出和错误输出各自定向至不同位置：
```
COMMAND >> /path/tofile.out 2>> /path/to/error.out
```
合并标准输出和错误输出为同一个数据流进行重定向
```
&>  // 合并数据流后，覆盖重定向
&>> // 合并数据流后，添加重定向
echo "$PATH" &> /tmp/path.out

COMMAND > /path/to/file.out 2> &1
COMMAND >> /path/to/file.out 2>> &1
```


输入重定向：`<`
从给定的地方读取数据。

```
cat < /etc/fstab /etc/issue
```

HARE Document：`<<`
```
cat >> /tmp/test.out << EOF // 给定字符之前键入的字符写入到文件中
```

## 管道

前一个命令的输出，当作后一个命令的输入。
连接N个命令

```
COMMAND1 | COMMAND2 | COMMAND3 | ...
```
最后一个命令会在当前`shell`进程的子进程中进行

```
echo "$PATH" | tr 'a-z' 'A-Z'
```

> tee

输入一份，标准输出和文件输出二份（覆盖输出）
```
tee /tmp/tee.out
```

```
head -n 5 /etc/passwd | tr 'a-z' 'A-Z' > /tmp/passwd.out
who | tail -n 2 | tr 'a-z' 'A-Z' > /tmp/who.out
```

## glob


`glob, globbing`

实现文件名“通配”

使用通配符：`*`, `?`, `[]`

`*`: 任意长度任意字符
`?`: 任意单个字符
`[]`: 指定范围内的任意单个字符
`[^]`: 指定范围之外的任意单个字符

专用字符集合：
```
[[:digit:]] = > [0-9] 

[:alnum:] 任意数值或字母 [:alpha:] 任意大小写字母  [:blank:]  [:cntrl:]
[:digit:] 任意数字 [:graph:]  [:lower:] 任意小写字母  [:print:]
[:punct:]标点符号  [:space:]  [:upper:] 任意大写字母 [:xdigit:]
```

## shell编程

`bash`提供了编程环境

程序：
- 算法 + 数据结构
- 指令 + 数据

程序编程风格：
- 过程式(面向过程)：以指令为中心，数据服务于指令
- 对象式(面向对象)：以数据为中心，指令服务于数据

shell程序：提供了编程能力，主要是当前系统上已有的二进制程序组织罗列，解析执行。


程序的执行方式：
计算机：运行二进制指令。

编程语言：
低级：汇编
高级：
	编译： 高级语言 --> 编译器 --> 目标代码. C,C++,Java
	解释：高级语言 --> 解释器 --> 机器代码. shell, perl, python

过程式编程：顺序执行，循环执行，选择执行

shell编程：过程式，解释执行。
严重依赖当前系统环境，shell编程实质是命令的堆砌。


`shell`脚本：文本文件

`shebang`机制：
告知CPU由哪个解释器执行
```
#!/bin/bash
#!/user/bin/ptyhon
#!/user/bin/perl
```

运行脚本：
- 给予执行权限，通过具体的文件路径指定文件执行
- 直接运行解释器，将脚本作为解释器程序的参数运行


编程程序语言：

- 强类型
- 弱类型： bash，把所有要存储的数据通通当作字符进行，不支持浮点数。


> 变量类型

数据存储格式
存储空间大小
参与运算种类


> bash中的变量的种类

根据变量的生效范围标准：
- 本地变量：当前shell进程，对当前shell之外的其它shell进程，包括当前shell的子进程均无效。声明`name=value`,使用`${name}`或者`$name`
- 环境变量：当前shell进程及其子进程有效。在脚本代码中调用通过命令行传递给脚本的参数。声明`declare -x name=bash`或者`export name=value`，使用`echo $name`.
- 局部变量：为当前shell进程中某代码片段（通常指函数上下文）
- 位置变量：$1,$2,...来表示，用于让脚本在脚本代码中调用通过命令行传递给它的参数。
- 特殊变量：$?(命令执行成功失败), $0(命令本身), $*(命令行传递的全部参数), $@(命令行传递的全部参数), $#(命令行传递的参数的个数)


显示已经定义的所有本地变量
```
> set
```
销毁本地变量
```
> unset name
```

显示所有环境变量：
```
export
env
printenv
```

只读变量 (shell进程销毁才能销毁只读变量)
```
readonly name
declare -r name
```

> bash配置文件

按生效范围划分：
- 全局配置
	`/etc/profile`, /etc/profile.d/*.sh, `/etc/bashrc`
- 个人配置
	`~/.bash_profile`, `~/.bashrc`

按功能划分：

- profile类：为交互式登录的shell提供配置
	全局：`/etc/profile`, `/etc/profile.d/*.sh`
	个人：`~/.bash_profile`
	功能：用于定义环境变量；运行命令或脚本。
- bashrc类：为非交互式登录的shell提供配置
	全局：`/etc/bashrc`
	个人：`~/.bashrc`
	功能：定义命令别名，定义本地变量


shell登录：
交互式登录：
	直接通过终端输入账号密码登录，使用`su - UserName`或`su -l UserName`切换的用户
	读取配置文件顺序：`/etc/profile` -> `/etc/profile.d/*.sh` -> `~/.bash_profile` -> `~/.bashrc` -> `/etc/bashrc`

非交互式登录：
	`su UserName`图形界面下打开的终端，执行脚本
	读取配置文件顺序：`~/.bashrc` -> `/etc/bashrc` -> `/etc/profile.d/*.sh`


定义对所有用户都生效的别名定义在：`/etc/bashrc`
用户登录都发出提示信息定义在： `/etc/profile.d/*.sh`
让用户的`PATH`环境变量的值多出一个路径。例如多出`/usr/local/apache/bin`

使配置文件生效：
```
source configFile
```

## bash脚本

> 算术运算

- let var=算数表达式
- var=$[算术表达式]
- var=$((算术表达式))
- var=$(expr arg1 arg2 arg3 ...); // var num=$(expr $num1 + $num2) // userid1=$(head -n 10 /etc/passwd | tail -n 1 | cut -d: -f3)


> 条件测试

判断某需求是否满足，需要由测试机制来实现

Note: 专用的测试表达式需要由测试命令辅助完成测试过程。

测试命令：
```
test EXPRESSION
[ EXPRESSION ] // 命令（前后需要有空格）
[[ EXPRESSION ]] // 关键字（前后需要有空格）

[1 -lg 3] // 1 > 3
[1 -gt 3] // 1 < 3
```

> bash测试类型

数值测试:
`-gt`, `-ge`大于等于, `-eq`等于, `-ne`不等于, `-lt`, `le`小于等于

字符串测试：
`==`, `>`, `<`, `!=`, `=~`左侧字符串是否能够被右侧的PTTERN所匹配到, `-z "STRING"`测试字符串是否为空，空为真，不空则为假, `-n "STRING"`测试字符串是否不空，不空则为真，空则为假 // [[ "str" =~ ^s.* ]]

文件测试：

> bash自定义退出状态码

```
exit [n]
```
注意：脚本中一旦遇到`exit`命令，脚本会立即终止，终止退出状态取决于`exit`命令后面的数字

```
[ $# -lt 1 ] && echo "At least one argument." && exit 1
```

## if语句

```
if 条件;
then
	分支代码
fi
```

添加用户：
```
#!/bin/bash

if [ $# -lt 1 ]; then
	echo "At least one arguments"
	exit 1
fi


if id $1 &> /dev/null; then
	echo "$1 exists."
	echo 0
else
	useradd $1
	[ $? -eq 0 ] && echo "$1" | passwd --stdin $1 &> /dev/null
fi
```
各种可能的情况想到，用户给任何一种信息都需要做判断。

