# VPN 搭建  
```  
docker run -v $PWD/data:/etc/openvpn --rm kylemanna/openvpn ovpn_genconfig -u udp://192.168.1.4

docker run -v $PWD/data:/etc/openvpn --rm -it kylemanna/openvpn ovpn_initpki

``` 

升级 Debian 11 -> Debian 12 参考: https://zhuanlan.zhihu.com/p/636675047

add-apt-repository -y ppa:nemh/systemback
repository: /etc/apt/sources.list.d


install gitlab 
https://docs.gitlab.com/ee/install/

```  
# password is in this file  
/etc/gitlab/initial_root_password
```  

docker 随容器启动
```  
docker update --restart=on-failure:10 <container name>
```

编译成镜像：

docker build -t <new img name>

删除无用的images： docker images prune

related nodejs versions on dockerhub https://hub.docker.com/_/node/

## apt update  
apt-get下载包的位置：/var/cache/apt/archives
下载位置可以在 /etc/apt/source.list 文件中指定