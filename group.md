
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
用户名:加密后密码:

加密机制：单向加密（提取数据指纹）
`md5: message digst, 128bits`
