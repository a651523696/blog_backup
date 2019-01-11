---
title: 配置git代理
date: 2019-01-11 14:03:23
tags: [git,proxy]
---

以下情况假设本机已搭建socks代理并开放端口1080
## 配置http协议代理
`git config --global http.proxy socks5://127.0.0.1:1080`
这样所有的通过http协议的操作都走了代理<!--more-->
取消代理
`git config --global --unset http.proxy`
## 如果只对github.com
`git config --global http.https://github.com.proxy socks5://127.0.0.1:1080`

取消代理
`git config --global --unset http.https://github.com.proxy`
如果其他域名要配置代理,同理


## 配置ssh协议代理
如果是走ssh协议,也就是clone的是此类地址git@github.com:xxx的话,需要在~/.ssh/config的指定Host下加一句
`ProxyCommand nc -X 5 -x localhost:1080 %h %p`,配置文件如下,以下是只针对github.com这个域名,如果想要其他域名走代理,同理配一个Host即可
```
Host github.com
        Hostname github.com
        User git
        Identityfile ~/.ssh/github/id_rsa
        ProxyCommand nc -X 5 -x 127.0.0.1:1080 %h %p
```
不过前提是你的终端里有__nc__命令