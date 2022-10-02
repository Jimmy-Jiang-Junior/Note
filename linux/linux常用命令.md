# Linux常用命令

## 1. 用ll代替“ls -l"

	ll并不是linux下一个基本的命令，它实际上是ls -l的一个别名。
	ubuntu默认不支持命令ll, 必须用ls -l, 这样使用起来不是很方便。
	如果要使用此命令，可以作如下修改：
	打开~/.bashrc
	找到#alias ll = 'ls -l', 去掉前面的#就可以了。


## 2. 配置Linux的路径显示

	修改环境变量PS1(命令行提示符), 在~/.bashrc末尾添加：
	export PS1='[\u\h:\W]\$'
	\u: 显示当前用户账号
	\h: 显示当前主机名
	\w: 显示当前完整工作路径
	\W: 显示当前工作路径
	\$: 显示'$'符号

## 4. samba使用

1. 查看samba服务器中已拥有哪些用户
   pdbedit -L

2. 删除用户
    smbpasswd -x   用户名

3. 添加用户
    smbpasswd -a 用户名(必须是linux用户）

4. samba服务重启 

  sudo /etc/init.d/samba restart

## 5. 生成ssh key

ssh-keygen -t rsa -C "577220709@qq.com"

## 6. rpm包解压命令

```shell
rpm2cpio xxx.rpm | cpio -div
```

## 7. make headers_install命令的作用是什么？

## 8. ls无颜色

与bashrc配置有关，如果/root目录下无bashrc，将用户目录下的bashrc拷贝到root目录下

