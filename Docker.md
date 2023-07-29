# Docker 常用命令

## copy 文件到指定容器

``` 
# 获取文件长名
docker inspect -f '{{.ID}}' <容器名>
# copy
docker cp <本地路径> <容器长ID>:<容器地址>
```

