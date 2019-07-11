---
layout: post
title: SpaceVim安装以及配置
date: 2019-07-11
Author: DLyn
categories: 
tags: [开发环境, linux, vim]
comments: true
---
### 1. 安装
**Linux 或 macOS**
```
curl -sLf https://spacevim.org/cn/install.sh | bash
```
安装结束后，初次打开 Vim 或者 gVim 时，SpaceVim 会自动下载并安装插件。
如果需要获取安装脚本的帮助信息，可以执行如下命令，包括定制安装、更新和卸载等。

```
curl -sLf https://spacevim.org/cn/install.sh | bash -s -- -h
```
**Windows**
Windows 

下最快捷的安装方法是下载安装脚本 [install.cmd](https://spacevim.org/cn/install.cmd) 并运行。

### 2. 配置
- **配置文件位置**
```
 ~/.SpaceVim.d/init.toml
```
- **配置绝对行号**

```
[options]
    relativenumber = false
```
- **配置语言支持**
```
# vue
[[layers]]
    name = 'lang#vue'
    
# golang
[[layers]]
    name = 'lang#go'
```