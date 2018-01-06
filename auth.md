
## 权限

文件的权限主要针对三类对象进行定义：

- owner：属主, u
- group：属组, g
- other：其它, o

每个文件正对每类访问者都定义了三种权限：

- r: Readable 可读
- w: Writable 可写
- x: eXcutable 可执行

文件：
- r: 可使用文件查看类工具获取其内容
- w：可修改其内容
- x: 可以把此文件提请内核启动为一个进程

目录：
- r: 可以使用l查看此目录中文件列表
- w：可在此目录中创建文件，也可删除此目录中的文件
- x: 可以使用ls -l 查看此目录中文件列表，可以cd进去此目录

对应二进制，八进制
```
--- 000 0
--x 001 1
-w- 010 2
-wx 011 3
r-- 100 4
r-x 010 5
rw- 110 6
rwx 111 7
```
-----
```
644
110 100 100
rw- r-- r--
664
110 110 100
rw- rw- r--
```

## 修改文件权限

`chmod [OPTION]... MODE[,MODE]... FILE...`
```
MODE:
u=rx
g=
o=
ug= // 二类用户一样
a= // 三类用户都一样
u=,g= // 二类用户不一样

// 修改一类用户某位或某些位权限
chmod u+w,o+r a.txt
u+
u-
g+
g-
o+
o-
a+
a-
ug+
u,g+ 
```

`chmod [OPTION]... OCTAL-MODE FILE...`
`-R`: 递归修改权限


`chmod [OPTION]... --reference=RFILE FILE...`
参考`REFILE`文件权限修改
`chmod --reference=b.txt a.txt`


## 修改文件的属主和属组
仅root可用：

`chown`: 修改文件的属主和属组
`chown [OPTION]... [OWNER][:[GROUP]] FILE...`
```
OWNER
OWNER:GROUP
:GROUP

chown admin:admin a.txt
chown :admina.txt
```
`-R`: 递归

`chown [OPTION]... --reference=RFILE FILE...`
参考`REFILE`文件权限修改

`chgrp`：修改文件的属组


## 遮罩码

文件或目录创建时的遮罩码：`umask`

FILE: 666 - umask : 如果某类用户的权限减得的结果中存在x权限，则x+
DIR: 777 - umask

`umask`: 查看
`umask 3`：设定

Note: `umask`仅对当前用户的当前`shell`有效, 如果需要有效，修改配置文件

