# WSL换源

https://docs.microsoft.com/zh-cn/windows/wsl/install

wsl 安装指导



新安装了WSL-Ubuntu默认的apt源是国外的源。国内访问速度会很慢。所以更改国内源是非常有必要的。

备份源列表文件

```
cd /etc/apt/
sudo cp sources.list sources.list.bak
```

修改源列表文件

```
sudo vim sources.list
```

将里面的内容全部删除，然后替换为阿里源

```
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
```

更改软件列表

```
sudo apt-get update
sudo apt-get upgrade
```

