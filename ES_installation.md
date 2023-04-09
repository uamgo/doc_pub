# ES 安装  

## 安装过程
```  
#下载镜像文件  
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.5.2

#单点运行
docker run --name elasticsearch -p 9200:9200  -p 9300:9300 \
       -e "discovery.type=single-node" \
       -e ES_JAVA_OPTS="-Xms84m -Xmx512m" \
       -v /home/ooo/share/es_docker/data:/usr/share/elasticsearch/data  \
       -v /home/ooo/share/es_docker/plugins:/usr/share/elasticsearch/plugins  \
       -d docker.elastic.co/elasticsearch/elasticsearch:7.5.2
#进入es容器
docker exec -it elasticsearch /bin/bash
#把config 拷贝到共享目录
cp -rf /usr/share/elasticsearch/config /usr/share/elasticsearch/data
cp /home/ooo/share/es_docker/data/config/* /home/ooo/share/es_docker/config
#回到宿主机，删原有容器
docker stop elasticsearch
docker rm elasticsearch
#重新启动
docker run --name elasticsearch -p 9200:9200  -p 9300:9300 \
       -e "discovery.type=single-node" \
       -e ES_JAVA_OPTS="-Xms84m -Xmx512m" \
       -v /home/ooo/share/es_docker/config:/usr/share/elasticsearch/config \
       -v /home/ooo/share/es_docker/data:/usr/share/elasticsearch/data  \
       -v /home/ooo/share/es_docker/plugins:/usr/share/elasticsearch/plugins  \
       -d docker.elastic.co/elasticsearch/elasticsearch:7.5.2


```  

## 安装管理界面  
### 安装
```  
docker pull mobz/elasticsearch-head:5
docker run -d --name es-head -p 9100:9100 docker.io/mobz/elasticsearch-head:5
```  

### 配置ES yml 
```   
vim /home/ooo/share/es_docker/data/config
```  
添加如下配置：
```  
http.cors.enabled: true   
http.cors.allow-origin: "*"
```  
### 重新启动ES  
```  
docker restart elasticsearch
```  


## 常见问题  
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