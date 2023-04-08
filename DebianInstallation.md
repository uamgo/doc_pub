# Debian installation 

## Mac 制作 Debian U盘 启动盘  

Debian 下载地址: [https://www.debian.org/distrib/](url)  
  
使用 dd 命令

最方便的是系统自带的 dd 命令。
首先需要将镜像从 ISO 转换为一个 UDRW (读写通用磁盘镜像格式)，Mac OS X 提供了将ISO镜像转换为UDRW 所需的所有工具。下面的命令将ISO镜像转换为 UDRW 格式。

1
$ hdiutil convert -format UDRW -o destination_file.img source_file.iso

要准备U盘, 我们将删除U盘上的所有分区, 并创建一个空分区。首先我们需要知道U盘的设备名称。打开一个终端并执行以下命令:

1
$ diskutil list

使用以下命令, 磁盘上的数据 (您的U盘) 将被删除!

1
$ diskutil partitionDisk /dev/disk2 1 "Free Space" "unused" "100%"

实行上面的命令, U盘被重新划分为有1分区, 没有格式化, 100% 的大小都用于这个分区。可以用 diskutil list 再次检查, 看看显示分区的变化。
将镜像复制到U盘上，此处替换您的U盘的相应磁盘名称

1
$ sudo dd if=destination_file.img.dmg of=/dev/disk2 bs=2m

dd 命令在完成复制过程之前不会显示任何输出, 因此请耐心等待它完成。

1
$ diskutil eject /dev/disk2

要弹出U盘, 请使用上面的命令。完成此操作后, 可启动的U盘已准备就绪。

## Debian configuration  

### 安装包源
/etc/apt/sources.list  
```  
deb http://mirrors.aliyun.com/debian/ bullseye main non-free contrib
deb-src http://mirrors.aliyun.com/debian/ bullseye main non-free contrib
deb http://mirrors.aliyun.com/debian-security/ bullseye-security main
deb-src http://mirrors.aliyun.com/debian-security/ bullseye-security main
deb http://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib
deb-src http://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib
deb http://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib
deb-src http://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib
deb http://mirrors.163.com/debian/ bullseye main non-free contrib
deb http://mirrors.163.com/debian/ bullseye-updates main non-free contrib
deb http://mirrors.163.com/debian/ bullseye-backports main non-free contrib
deb-src http://mirrors.163.com/debian/ bullseye main non-free contrib
deb-src http://mirrors.163.com/debian/ bullseye-updates main non-free contrib
deb-src http://mirrors.163.com/debian/ bullseye-backports main non-free contrib
#deb http://mirrors.163.com/debian-security/ bullseye/updates main non-free contrib
#deb http://mirrors.ustc.edu.cn/debian-security/ bullseye/updates main non-free contrib
#deb-src http://mirrors.163.com/debian-security/ bullseye/updates main non-free contrib
#deb-src http://mirrors.ustc.edu.cn/debian-security/ bullseye/updates main non-free contrib
deb http://mirrors.ustc.edu.cn/debian-security/ stable-security main non-free contrib
deb-src http://mirrors.ustc.edu.cn/debian-security/ stable-security main non-free contrib

```  
### 必要的安装包  
```  
apt-get update  
apt-get install vim  
apt-get install openssh-server
```  
### ssh 配置  
``` 
vim /etc/ssh/sshd_config 

# 开启这个选项  
PermitRootLogin yes

# 重启ssh
/etc/init.d/ssh restart
# 检查ssh状态
/etc/init.d/ssh status
``` 
### 修改普通用户无密码 sudo  
```  
sudo visudo

# 增加自己的用户
<user name>   ALL=(ALL:ALL) NOPASSWD: ALL
``` 

### 关闭休眠  
```  
#查看休眠设置
sudo systemctl status sleep.target

#停止休眠
sudo systemctl mask sleep.target suspend.target hibernate.target hybird-sleep.target
```  



