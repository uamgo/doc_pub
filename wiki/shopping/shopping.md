# 商城小程序总结  
```  
#淘宝源  
npm config set registry https://registry.npmmirror.com  

# 恢复国内源  
npm config set registry https://registry.npmjs.org  
```  
npm 源参考文档：https://zhuanlan.zhihu.com/p/623547625

## hioshop-server  
按 github 要求初始化数据库 -> 修改mysql 地址 ->启动服务

修改 mysql 地址  :src/common/config/database.js
```  
const mysql = require('think-model-mysql');

module.exports = {
    handle: mysql,
    database: 'hiolabsDB',
    prefix: 'hiolabs_',
    encoding: 'utf8mb4',
    host: '127.0.0.1',
    port: '3306',
    user: 'root',
    password: '123123', //你的密码
    dateStrings: true
};
```  


https://github.com/iamdarcy/hioshop-server  

#### 问题一：ER_NOT_SUPPORTED_AUTH_MODE 

```  
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';   
``` 

## hioshop-admin-web  
接口对应的IP改为本地IP：./src/config/api.js
```  
//const rootUrl = 'https://www.guzong1.com:446/admin/';
const rootUrl = 'http://192.168.1.4:8360/admin/';
```  
初始用户名密码：hiolabs/hiolabs


ctnet