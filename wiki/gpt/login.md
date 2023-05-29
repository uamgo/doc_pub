# 掉线后重新登录

## 目标

* 快速恢复，保障业务连续性

## 详细步骤

1. xshell 登录服务器

2. 执行命令查看二维码

   ```shell
   tail -n 100 /var/log/chatgpt/chatgpt.log
   ```

3. 扫描二维码，确认并登录
4. 测试“理查德”



## 其他常见问题

* 登录后仍然不起作用，怎么办？

  * 重启服务

    ```shell
    cd chatgpt-on-wechat && sh restart.sh
    ```

  		* 再次查看二维码、扫描登录、测试

