# VPS 自用常用脚本

## 基础

-  ### 创建root用户密码

```
echo root:'密码' |sudo chpasswd root
sudo sed -i 's/^.*PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config;
sudo sed -i 's/^.*PasswordAuthentication.*/PasswordAuthentication yes/g' /etc/ssh/sshd_config;
sudo service sshd restart
```

-  ### 安装curl和weget

***Centos***

```
yum install -y curl wget 2> /dev/null
```

***Ubuntu***

```
apt install -y curl wget
```

-  ### 安装ca-certificates

***Centos***

```
yum install -y ca-certificates
```

***Ubuntu***

```
apt install -y ca-certificates
```

-  ### 管理BBR加速

首次使用

```
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

后续使用

```
./tcp.sh
```

-  ### 安装哪吒面板

首次使用

```
curl -L https://raw.githubusercontent.com/naiba/nezha/master/script/install.sh -o nezha.sh && chmod +x nezha.sh && ./nezha.sh
```

后续使用

```
./nezha.sh
```

-  ### 安装screen

***Centos***

```
yum install -y screen
```

***Ubuntu***

```
apt install -y screen
```

使用方法

```
screen #创建一个新的窗口
screen -ls #列出所有窗口
screen -wipe #删除Dead窗口
screen -r 123 #回到窗口123
screen -d 123 #分离123 窗口
screen -S 123 -X quit #杀死窗口123
```

-  ### 安装nano编辑器

***Centos***

```
yum install -y nano
```

***Ubuntu***

```
apt install -y nano
```

-  ### 安装unzip

***Centos***

```
yum install -y unzip
```

***Ubuntu***

```
apt install -y unzip
```

-  ### 安装unrar

***Centos***

下载rar安装包

```
wget https://www.rarlab.com/rar/rarlinux-x64-6.0.2.tar.gz --no-check-certificate
```

解压压缩包到/usr/local下

```
tar zxvf rarlinux-x64-6.0.2.tar.gz -C /usr/local
```

将 rar 和 unrar 命令链接到/usr/local/bin目录下

```
ln -s /usr/local/rar/rar /usr/local/bin/rar
ln -s /usr/local/rar/unrar /usr/local/bin/unrar
```

***Ubuntu***

```
apt-get install -y unrar
apt-get install -y rar
```

查看帮助文档

```
rar --help
unrar --help
```

使用方法

```
unrar x '文件目路径.rar' '保存的路径'
```

-  ### 安装7zip

***Centos***

```
yum install -y epel-release
yum install -y p7zip p7zip-plugins
```

***Ubuntu***

```
add-apt-repository universe
apt install -y p7zip-full p7zip-rar
```

使用方法

```
7z x '压缩文件路径' -r -o/'需要保存到的路径'
```

- ### 更改时区

更改到上海

```
timedatectl set-timezone 'Asia/Shanghai'
```

## 常用应用

-  ### Aria2

为了确保能正常使用，请先安装基础组件wget、curl、ca-certificates

```
yum install -y wget curl ca-certificates #Centos
apt install -y wget curl ca-certificates #Ubuntu
```

下载脚本

```
wget -N git.io/aria2.sh && chmod +x aria2.sh
```

运行脚本

```
./aria2.sh
```

修改配置文件

```
nano /root/.aria2c/aria2.conf
```

配置完成下载后自动上传

找到“**下载完成后执行的命令**”，把**clean**.sh替换为**upload**.sh

```
on-download-complete=/root/.aria2c/upload.sh
```

修改附加脚本配置

```
nano /root/.aria2c/script.conf
```

修改完成后重启Aria2

```
service aria2 restart
```

检查配置是否成功

```
/root/.aria2c/upload.sh
```

Aria2 配置参考

[Aria2.conf](https://github.com/Rex0929/VPS/blob/main/aria2.conf)

[Script.conf](https://github.com/Rex0929/VPS/blob/main/script.conf)

-  ### Rclone

一键安装Rclone

```
curl https://rclone.org/install.sh | sudo bash
```

配置Rclone

```
rclone config
```

Rclone 配置参考

[参考配置](https://github.com/Rex0929/VPS/blob/main/Rclone.md)

- ### 使用Rclone将文件上传至网盘

使用screen后台上传

```
screen rclone move -v /DISK/downloads OneDriveE51:/upload --transfers 2 -P
```

- ### SS-GO

首次使用

```
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/ss-go.sh && chmod +x ss-go.sh && bash ss-go.sh
```

后续使用

```
./ss-go.sh
```

- ### 流媒体检测

```
bash <(curl -L -s https://raw.githubusercontent.com/lmc999/RegionRestrictionCheck/main/check.sh)
```

- ### ToolBox

首次使用

```
wget -O jcnfbox.sh https://raw.githubusercontent.com/Netflixxp/jcnf-box/main/jcnfbox.sh && chmod +x jcnfbox.sh && clear && ./jcnfbox.sh
```

后续使用

```
./jcnfbox.sh
```

- ### 多维度测试VPS

```
bash <(wget -qO- --no-check-certificate https://gitlab.com/spiritysdx/za/-/raw/main/ecs.sh)
```

- ### 测试部分游戏延迟

```
bash <(curl -L -s https://raw.githubusercontent.com/lmc999/GamePing/main/GamePing.sh)
```

- ### 安装Socks5代理

下载脚本

```
wget --no-check-certificate https://raw.github.com/Lozy/danted/master/install.sh -O install.sh
```

安装脚本

```
bash install.sh  --port=运行端口 --user=用户名 --passwd=密码
```

卸载脚本

```
bash install.sh --uninstall
```

- ### Soga后端

下载脚本

```
bash <(curl -Ls https://github.com/sprov065/soga/raw/master/soga.sh)
```

编辑soga配置文件

```
nano  /etc/soga/soga.conf
```

后续运行

```
soga
```

- ### XrayR后端

下载脚本

```
bash <(curl -Ls https://raw.githubusercontent.com/XrayR-project/XrayR-release/master/install.sh)
```

编辑XrayR配置文件

```
nano  /etc/XrayR/config.yml
```

后续运行

```
xrayr
```

- ### 一键WARP脚本

```
wget -N https://cdn.jsdelivr.net/gh/fscarmen/warp/menu.sh && bash menu.sh
```

WARP菜单

```
bash menu.sh
```

- ### Prename

***Centos***

```
yum install -y epel-release
yum install -y prename
```

使用方法

```
prename -v 's/原字符串表达式1/目标字符串表达式2/' 文件(列表)
```

- ### Rename

***Ubuntu***

```
apt install -y rename
```

使用方法

```
rename 原字符串 目标字符串 文件(列表)
```

- ### BestTrace

下载脚本

```
wget https://cdn.ipip.net/17mon/besttrace4linux.zip
mkdir besttrace
unzip besttrace4linux.zip -d ./besttrace
cd besttrace
chmod 755 besttrace
```

运行脚本

```
./besttrace/besttrace -q 1 'Your=IP'
```

- ### SpeedTest CLI

***Centos***

安装脚本

```
curl -s https://packagecloud.io/install/repositories/ookla/speedtest-cli/script.rpm.sh | sudo bash
yum install -y speedtest
```

***Ubuntu***

```
curl -s https://packagecloud.io/install/repositories/ookla/speedtest-cli/script.rpm.sh | sudo bash
apt install -y speedtest
```

使用方法

```
speedtest
```

查看帮助

```
speedtest -h
```


## 系统

- ### 防火墙

***Centos***

查看防火墙状态

```
systemctl status firewalld
```

开启防火墙

```
systemctl start firewalld
```

临时关闭命令

```
systemctl stop firewalld
```

永久关闭命令

```
systemctl disable firewalld
```

***Ubuntu***

打开防火墙

```
sudo ufw enable
```

关闭防火墙

```
sudo ufw disable
```

- ### iptables

开放所有端口

```
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -F
```
