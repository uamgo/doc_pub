# 怎样在 mac 下方便的连接 

## 搜索打开Mac 命令行
command + space  
输入 “term”  回车

## 保存 ssh key(密码)
``` 
# ssh-copy-id <user name>@<ip>
E.g: 
ssh-copy-id root@1.1.1.1

 ```  
回车后 遇到如下提示，输入yes  
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/jully/.ssh/id_rsa.pub"
The authenticity of host '108.61.157.35 (108.61.157.35)' can't be established.
ECDSA key fingerprint is SHA256:LqfL0BnJy60Yacwd6o+xe4TjjKAg6LwcrCshcSsoojM.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
  
下一步输入提示输入密码, 输入正确的密码 
Password:  

命令执行完成  

## 登录服务器，在term 中输入如下命令登录  
```    
ssh root@1.1.1.1  
```


# 错误处理  

## 常见错误一： term 开始第一条命令，报ssh错误  
错误原因：大概率是没有在本机生成 ssh key  
解决办法：执行如下命令，一路回车即可   
```  
ssh-keygen -t rsa  
```


## 常见错误二：  vutlr 服务器重新安装了，地址未变，遇到如下错误  
错误原因：密码变化了，需要删除老密码，重新保存新密码  
解决办法：  
```  
vim ~/.ssh/known_hosts    
#输入 /108.61.157.35  填写自己的IP，回车  
#输入 dd   
#点击键盘上的 ESC  
#输入 shift + :  
#输入 x 回车  
```

➜  doc_pub git:(master) ssh root@108.61.157.35
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ED25519 key sent by the remote host is
SHA256:hgljWW0gwHO05FZiogu45MJtTafVvWiMMLf1Be+1BKk.
Please contact your system administrator.
Add correct host key in /Users/kevin/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /Users/kevin/.ssh/known_hosts:191
Host key for 108.61.157.35 has changed and you have requested strict checking.
Host key verification failed.

