---
layout: post
title: 开发环境-下载依赖包过慢
date: 2019-09-04
Author: DLyn
categories: 
tags: [开发环境, proxy, 依赖包]
comments: true
---

#### 国内Github访问过慢
1. 使用浏览器访问https://www.ipaddress.com/，分别获取github.com，github.global.ssl.fastly.net对应的ip，例如:
```bash
# github
192.30.253.112 github.com
151.101.13.194 github.global.ssl.fastly.net
```
2. 修改host文件
```bash
# Windows host 位置
/c/Windows/System32/drivers/etc
# Linux host 位置
/etc/hosts
```
3. 重启网络

#### Go语言依赖包下载
- 在Linux或macOS中，您可以执行以下命令。或者，将其写入.bashrc或.bash_profile文件。
```bash
# Enable the go modules feature
export GO111MODULE=on
# Set the GOPROXY environment variable
export GOPROXY=https://goproxy.io
```
- 在Windows中，您可以执行以下命令。
```powershell
# Enable the go modules feature
$env:GO111MODULE=on
# Set the GOPROXY environment variable
$env:GOPROXY=https://goproxy.io
```

- Go版本> = 1.13

GOPRIVATE环境变量控制go命令认为哪些模块是私有的（不公开），因此不应使用代理或校验和数据库。例如：
```bash
export GOPRIVATE=*.corp.example.com
```