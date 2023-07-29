# 股数据接口

## 目标  
>实现根据策略筛选并通过微信查询发送股票，符合以下条件：

>> 1. 日线，非10日内最低点
>> 2. 日线，非连续5日下跌
>> 3. 分时线，倒排时间序，找到最后一根高于平均10倍的
>> 4. 股价大于4元，注册制后，4元以下都是垃圾股
>> 5. 当日分时线量柱：绿柱 < 红柱*0.8
>> 6. 市值大于10亿，太小的盘子没必要做
>> 7. 量比大于1
>> 8. 不看科创板
>> 9. 这些股票代码都不看：'ST' in name or '退市' in name or 'N' in name or 'L' in name or 'C' in name or 'U'

>> 后续补充板块信息

## 安装准备
### 方式一  docker 安装方式  
```  
docker pull registry.cn-shanghai.aliyuncs.com/akfamily/aktools:jupyter
docker run -it registry.cn-shanghai.aliyuncs.com/akfamily/aktools:jupyter python
```

### 方式二 命令行安装  
```  
pip3 install akshare
pip3 install pandas
```

## 优化进展

* 单线程版本 v1.0.0
  * 耗时 146.77s
* 多线程
  * 耗时 36.44s，提升 (146.77 - 36.44)/146.77 = 75.17%
  * 每个线程 100 只股票，总计线程数 1790/100 +1 = 18
  * 1790只有效股票，总计5433只股票

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