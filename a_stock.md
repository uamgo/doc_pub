# 股数据接口

## 目标  
>实现根据策略筛选并通过微信查询发送股票，符合以下条件：

>> 1. 日线，非10日内最低点
>> 2. 日线，非连续5日下跌
>> 3. 分时线，倒排时间序，找到最后一根高于平均10倍的

>> 后续补充板块信息

## 安装准备
### 方式一  docker 安装方式  
```  
docker pull registry.cn-shanghai.aliyuncs.com/akfamily/aktools:jupyter
docker run -it registry.cn-shanghai.aliyuncs.com/akfamily/aktools:jupyter python
```  

### 方式二 命令行安装  
```  
pip install akshare
pip install pandas
``` 


## 参考文档

akshare使用文档说明：[https://akshare.akfamily.xyz/ ](url)   
akshare源码地址：[https://gitee.com/uamgo/akshare#https://gitee.com/link?target=https%3A%2F%2Fakshare.akfamily.xyz%2F](url)


## 备用参考  
### Debian 安装 python 环境  
```  
sudo apt-get install python3
sudo apt-get install python3-pip
```  

规则探索：
分时线，开盘收盘价相同，则和前值相比较，确定是红绿柱