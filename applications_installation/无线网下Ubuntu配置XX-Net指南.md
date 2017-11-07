# 无线网下Ubuntu配置XX-Net指南

## 1. 准备工作
> 由于Linux版的XX-Net是Python和shell脚本写的，所以Python2.7的配置环境是必须要完整的.

1) 一般来说，要手动安装以下一些依赖包和依赖扩展：

```shell
sudo apt-get install python-gtk2
sudo apt-get install python-openssl
sudo apt-get install libffi-dev
sudo apt-get install -y python-gtk2
sudo apt-get install python-appindicator
sudo apt-get install libnss3-tools
```
自动导入证书，需要安装libnss3-tools：
```shell
sudo apt-get install libnss3-tools
```
2)下载XX-Net源码包，可以去github上免费下载开源项目[XX-Net下载](https://github.com/XX-net/XX-Net/).
```shell
sudo git clone git@github.com:XX-net/XX-Net.git 或者 
sudo git clone https://github.com/XX-net/XX-Net.git
```
可以看到文件夹里面有可执行文件start和start.sh,后面会用到这两个文件.

## 2. IPv6的开启
> 新版的XX-Net只支持IPv6，当前教育网是默认支持IPv6的，但在无线网下，Ubuntu的IPv6服务默认是不存在的，所以要先通过虚拟的IPv6网卡转换IPv4的流量，使之可以使用IPv6.

1) 安装虚拟网卡teredo,首先查看是否已安装过teredo.
```shell
sudo dpkg -l | grep miredo
```
若没安装过，进行安装：
```shell
sudo apt install miredo
```
安装完成后，ifconfig查看，默认安装完毕后启动的，所以会看到一个叫teredo的网卡(虚拟的IPv6网卡).但是要注意的是，此网卡是重启后就失效的，所以每次重启务必记得打开网卡：
```shell
sudo miredo
```
2)教育网获取原生态IPv6的方法，详见：[IPv6的获取](https://github.com/tuna/ipv6.tsinghua.edu.cn/blob/master/isatap.md).不过不用担心，一般的教育网都是开通了IPv6服务的.

## 3. Chrome浏览器中SwitchyOmega扩展的安装
> 说到这儿，很多人会问了，我都没科学冲浪，又怎么能获取Google应用扩展呢？其实，只要你想，就会有一万种方法可以获得。这里介绍简单的办法.

下面的安装步骤将告诉你，在你的网络还没有能力访问Chrome的网上运用商店的做法：
直接抛链接了啦：[SwitchyOmega下载](https://github.com/FelisCatus/SwitchyOmega/releases),下载对应的版本导入即可，最好是最新版。
## 4. 开始科学冲浪
在步骤1中已经完成了下载源码和部署Python环境的基本操作，下面就是开始冲浪了.
进入XX-Net文件夹，运行start可执行程序：
```shell
sudo ./start
```
会在主窗口右上角出来XX的logo，和Windows下是一个样的，同时会在浏览器中弹出配置界面，地址一般是127.0.0.1:8085或者端口号是8086不等.
在界面里有Gaeproxy,xx-tunnel等基本方式，一般使用Gaeproxy代理.在配置里启用IPv6,开启一段时间，扫描足够多的IP地址，就可以科学冲浪了，速度还是不错的哦.
chrome 里的SwitchyOmega是用来控制代理流量的，可以选择不同的代理方式，决定是否科学冲浪.
注意：SwitchOmega里XX-Tunnel自动切换和GAE-Proxy自动切换是需要事先导入下面一段地址（直接复制到规则列表网址框里即可）的，用于更新相关规则的： ```https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt```
好了，到这里就全部讲完了，如有疑问，随时邮件交流：hmin@zju.edu.cn
