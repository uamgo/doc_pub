# supervisor 常见问题

## 安装

## 添加新命令

1. 在目录 /etc/supervisor/conf.d/ 下添加 .conf 结尾的文件，文件内容参考

```tex
[program:chatgpt]
directory =  /home/ooo/stock/supervisor; 程序的启动目录
command = sh start.sh ; 启动命令，可以看出与手动在命令行启动的命令是一样的
autostart = true ; 在 supervisord 启动的时候也自动启动
startsecs = 5 ; 启动 5 秒后没有异常退出，就当作已经正常启动了
autorestart = true ; 程序异常退出后自动重启
startretries = 9 ; 启动失败自动重试次数，默认是 3
user = root ; 用哪个用户启动
redirect_stderr = true ; 把 stderr 重定向到 stdout，默认 false
stdout_logfile_maxbytes = 200MB ; stdout 日志文件大小，默认 50MB
stdout_logfile_backups = 10 ; stdout日志文件备份数
; stdout 日志文件，需要注意当指定目录不存在时无法正常启动，所以需要手动创建目录>（supervisord 会自动创建日志文件）
stdout_logfile = /var/log/stock/stock.log

```

2. 检查文件是否有效

```shell
sudo supervisorctl reread
```

3. 添加命令

```
sudo supervisorctl update
```



## 常见错误

* 程序目录后面的分号前后要有空格，否则如下错误

supervisor: couldn't chdir to /home/ooo/stock/supervisor; 程序的启动目录: ENOENT

