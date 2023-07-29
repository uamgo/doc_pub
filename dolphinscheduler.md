# DolphinScheduler 部署



```shell
DOLPHINSCHEDULER_VERSION=3.1.7
docker run --name dolphinscheduler-standalone-server -p 12345:12345 -p 25333:25333 -d apache/dolphinscheduler-standalone-server:"${DOLPHINSCHEDULER_VERSION}"
```



安装 docker compose

```shell
sudo yum install docker-compose-plugin
```



安装 mysql

```
docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
```

初始化数据源

```
mysql -uroot -p

mysql> CREATE DATABASE dolphinscheduler DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;

# 修改 {user} 和 {password} 为你希望的用户名和密码
mysql> CREATE USER '{user}'@'%' IDENTIFIED BY '{password}';
mysql> GRANT ALL PRIVILEGES ON dolphinscheduler.* TO '{user}'@'%';
mysql> CREATE USER '{user}'@'localhost' IDENTIFIED BY '{password}';
mysql> GRANT ALL PRIVILEGES ON dolphinscheduler.* TO '{user}'@'localhost';
mysql> FLUSH PRIVILEGES;
```

然后修改`./bin/env/dolphinscheduler_env.sh`，将username和password改成你在上一步中设置的用户名{user}和密码{password}

对于 MySQL：

```
# for mysql
export DATABASE=${DATABASE:-mysql}
export SPRING_PROFILES_ACTIVE=${DATABASE}
export SPRING_DATASOURCE_URL="jdbc:mysql://127.0.0.1:3306/dolphinscheduler?useUnicode=true&characterEncoding=UTF-8&useSSL=false"
export SPRING_DATASOURCE_USERNAME={user}
export SPRING_DATASOURCE_PASSWORD={password}
```

修改springboot 数据源 conf/application.yaml

改为：mysql驱动

配置hdfs

conf/common.properties中配置



配置network

``` shell
docker network connect hadoop_default mysql-test 
docker network connect dolphinscheduler-standalone-server
```



编译任务

需要安装maven，并配置 ali mirror https://developer.aliyun.com/mirror/maven?spm=a2c6h.13651102.0.0.7be81b113zlrM0

```shell
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
cd /tmp
git clone https://github.com/uamgo/test.git hello
cd hello
/tmp/maven/bin/mvn clean package -Dmaven.repo.local=/tmp/repo
ls -la target
```



## 参考文档

https://dolphinscheduler.apache.org/zh-cn/docs/3.1.7/guide/start/docker

https://docs.docker.com/compose/install/linux/

https://github.com/apache/dolphinscheduler/blob/3.1.7-release/docs/docs/zh/guide/howto/datasource-setting.md