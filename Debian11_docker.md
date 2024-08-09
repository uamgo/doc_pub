# Debian 11 安装Docker

虽然kubernetes早在2018年5月就宣布用户可以不用安装docker，直接使用containerd作为CRI运行时，docker依然在生产环境中有很高的装机量，并且在单机开发环境中使用docker相对containerd更为方便。因此在2021年docker依然有其存在价值。

2021年8月，debian11终于发布，本文描述如何在debian11上安装docker，可以参考官方文档。

安装基础工具  
```  
sudo apt-get update
 sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
2. 安装docker的gpg key：  
```  

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
3. 安装docker源
```  
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
#上面命令中的lsb_release -cs返回bullseye，也就是debian11的代号。
```
4. 安装docker
```  
apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
至此安装完成。

在debian系的Linux发行版上，docker会开机启动启动。

如果平时使用非root账户，又不想每次执行docker命令之前都加上sudo，参考docker的文档，可以添加docker组，并将非root账户加入到该组中。下面的命令创建docker组并将当前用户加入docker组，执行完成之后重新登陆生效：
```  
sudo groupadd docker
sudo usermod -aG docker $USER

#重启docker
sudo systermctl restart docker
#开机自启动docker
sudo systermctl enable docker
```

阿里源环境安装 docker

```
curl -sSL https://mirrors.aliyun.com/docker-ce/linux/debian/gpg | gpg --dearmor > /usr/share/keyrings/docker-ce.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-ce.gpg] https://mirrors.aliyun.com/docker-ce/linux/debian $(lsb_release -sc) stable" > /etc/apt/sources.list.d/docker.list
apt update
apt-get install docker-ce docker-ce-cli containerd.io
apt-get install docker-compose-plugin
```

