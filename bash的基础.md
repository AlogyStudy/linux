

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

