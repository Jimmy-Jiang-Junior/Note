# raspberry使用问题记录

https://wiki.diustou.com/cn/%E6%A0%91%E8%8E%93%E6%B4%BE%E7%B3%BB%E5%88%97%E6%95%99%E7%A8%8B%EF%BC%9A%E8%BF%9C%E7%A8%8B%E7%99%BB%E5%BD%95%E6%A0%91%E8%8E%93%E6%B4%BE

树莓派链接

## 1. wifi无法配置

参考：https://blog.csdn.net/qq1140920745/article/details/110826222
ifconfig看不到wlan0相关信息
（1）使用sudo ifconfig -a可以看到有wlan0,证明网卡驱动没问题，只是无线射频被
锁起来了，使用rfkill list查看是否关闭射频：
（2）可以使用rfkill unblock all全部打开，再ifconfig看一下，可以看到有wlan0
（3）配置wifi连接网络
	vim /etc/wpa_supplicant/wpa_supplicant.conf
	添加完网络配置
	network={
		ssid="WIFI名"
		psk="WIFI密码"
	}
	注意要使用TAB键
（4）reboot之后使用ifconfig命令就可以看到wlan0分配了ip地址
（5）通过ssh登陆ip地址即可

## 2. raspberry上安装docker

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

## 3. 树莓派的默认账户密码

User: pi

Passwd: raspberry