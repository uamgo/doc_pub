# ES 安装  

Error response from daemon: Get "https://docker.elastic.co/v2/": net/http: TLS handshake timeout

TLS握手超时

拉取镜像遇到这几个问题，原因基本都是因为从国外拉取镜像，访问速度太慢导致要么超时，要么请求中断，解决方法就是使用加速器来解决。

首先打开配置文件daemon.json，centos上安装后有此文件，但是ubuntu上需要自己创建文件：  

操作：vim  /etc/docker/daemon.json   

在文件中加入：
```  

{
    "registry-mirrors":["https://docker.mirrors.ustc.edu.cn"]
}
```  

 重启守护进程：
```  

sudo systemctl daemon-reload
sudo systemctl restart docker
```  