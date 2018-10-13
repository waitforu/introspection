# Linux命令

## 用户相关
> groups查看当前登录用户的组内成员;
> groups username查看`username`用户所在组，及组内成员;
> whoami查看当前登录的用户名
```
附：
/etc/group文件包含所有组
/etc/shadow和/etc/passwd系统存在的所有用户名
```
> 用户管理
```
useradd/adduser 注：添加用户（常用的几个参数）
	-d：指定用户登入时的主目录，替换系统默认值/home/<用户名>
	-f：指定在密码过期后多少天即关闭该账号。如果为0账号立即被停用；如果为-1则账号一直可用。默认值为-1.
	-g：指定用户所属的群组。值可以使组名也可以是GID。用户组必须已经存在的，期默认值为100，即users。
	-m：自动建立用户的登入目录。
	-n：取消建立以用户名称为名的群组。
	-r：建立系统账号。
	-s：指定用户登入后所使用的shell。默认值为/bin/bash。
	例：useradd -d /var/www/html/admin -g webadmins -m webadmin1
userdel (-f) 删除用户(强制删除并登出)
passwd 注：为用户设置密码
usermod 注：修改用户命令，可以通过usermod 来修改登录名、用户的家目录等等；
su 注：用户切换工具 sudo 注：sudo 是通过另一个用户来执行命令（execute a command as another user），su 是用来切换用户，然后通过切换到的用户来完成相应的任务，
但sudo 能后面直接执行命令，比如sudo 不需要root 密码就可以执行root 赋与的执行只有root才能执行相应的命令；但得通过visudo 来编辑/etc/sudoers来实现；
```
> 用户组管理
```
groupadd 添加用户组
	-g 指定组ID号。
groupdel 删除用户组
groupmod 修改用户组信息
	-n 设置新的用户组名
```