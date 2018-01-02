
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