---
layout: post
title: Github仓库clone代理设置
date: 2020-09-03
Author: DLyn
categories: 
tags: [Github, 开发环境, 镜像/代理]
comments: true
---

## 分辨需要设置的代理

- HTTP 形式：
   > git clone https://github.com/owner/git.git
- SSH 形式：
   > git clone git@github.com:owner/git.git

## 一、HTTP 形式
### 走 HTTP 代理

```bash
git config --global http.proxy "http://127.0.0.1:8080"
git config --global https.proxy "http://127.0.0.1:8080"
```

### 走 socks5 代理（如 Shadowsocks）

```bash
git config --global http.proxy "socks5://127.0.0.1:1080"
git config --global https.proxy "socks5://127.0.0.1:1080"
```

### 取消设置

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

## 二、SSH 形式

修改 `~/.ssh/config` 文件（不存在则新建）：

```
# 必须是 github.com
Host github.com
   HostName github.com
   User git
   # 走 HTTP 代理
   # ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=8080
   # 走 socks5 代理（如 Shadowsocks）
   # ProxyCommand nc -v -x 127.0.0.1:1080 %h %p
```

### 额外说明
对于Windows用户，要使用socks5代理却没有 nc 的，可以将
```
ProxyCommand nc -v -x 127.0.0.1:1080 %h %p
```
换成
```
ProxyCommand connect -S 127.0.0.1:1080 %h %p
```

### 其他配置
```
Host github.com
    User git
    Port 22
    Hostname github.com
    IdentityFile "/home/glink/.ssh/id_rsa"
    TCPKeepAlive yes
    ProxyCommand nc -v -x 127.0.0.1:1080 %h %p

Host ssh.github.com
    User git
    Port 443
    Hostname ssh.github.com
    IdentityFile "/home/glink/.ssh/id_rsa"
    TCPKeepAlive yes
    ProxyCommand nc -v -x 127.0.0.1:1080 %h %p

Host *
    KexAlgorithms +diffie-hellman-group1-sha1
```
