# wechat chatgpt  
## 安装过程  
```  

apt-get install git
git clone https://github.com/zhayujie/chatgpt-on-wechat

pip3 install itchat-uos==1.5.0.dev0
pip3 install --upgrade openai

cp config-template.json config.json

# 修改允许 chat gpt的群名
vim config.json  

#找到while not isLoggedIn: 这行，在这行前面加上  time.sleep(15)
find /usr/local/lib/python3.9/dist-packages -name ‘login.py'
vim /usr/local/lib/python3.9/dist-packages/itchat/components/login.py

#安装守护进程
apt-get install supervisor

#创建守护进程执行chatgpt的说明文件
cat << "EOF" > /etc/supervisor/conf.d/chatgpt.conf
[program:test]
directory = /usr/local ; 程序的启动目录
command =  python3 /root/chatgpt-on-wechat/app.py ; 启动命令，可以看出与手动在命令行启动的命令是一样的
autostart = true ; 在 supervisord 启动的时候也自动启动
startsecs = 5 ; 启动 5 秒后没有异常退出，就当作已经正常启动了
autorestart = true ; 程序异常退出后自动重启
startretries = 9 ; 启动失败自动重试次数，默认是 3
user = root ; 用哪个用户启动
redirect_stderr = true ; 把 stderr 重定向到 stdout，默认 false
stdout_logfile_maxbytes = 200MB ; stdout 日志文件大小，默认 50MB
stdout_logfile_backups = 10 ; stdout日志文件备份数
; stdout 日志文件，需要注意当指定目录不存在时无法正常启动，所以需要手动创建目录>（supervisord 会自动创建日志文件）
stdout_logfile = /var/log/chatgpt/chatgpt.log
EOF

mkdir  /var/log/chatgpt
supervisorctl update
supervisorctl reload
```  

## 相关文档  
获取api key 的连接：
[https://platform.openai.com/account/api-keys](url)

