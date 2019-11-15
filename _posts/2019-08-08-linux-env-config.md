---
layout: post
title: Linux常见环境问题汇总
date: 2019-08-08
Author: DLyn
categories: 
tags: [开发环境, linux]
comments: true
---

#### 设置PATH
```
export PATH="$PATH:/opt/android-studio/bin"
```
#### 设置NVM
```
export NVM_DIR="/home/dlyn/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
```
#### 常用配置
```
# set proxy
alias setproxy='export ALL_PROXY=socks5://127.0.0.1:1080'
alias unsetproxy='unset ALL_PROXY'

# set open just like in OSX
alias open='xdg-open'

#　go env (version > 1.13)
export GO111MODULE=on
export GOPROXY=https://goproxy.io
export GOPRIVATE=*.corp.example.com
```
#### Linux搜狗输入法候选词乱码

```
cd ~/.config
sudo rm -rf SogouPY* sogou*
```
然后注销即可(注意，这里必须是注销，不注销直接重启并不管用)

#### 网易云音乐启动不了

1. 安装 `libcanberra-gtk-mod`

```
sudo apt install libcanberra-gtk-module
```
2. 修改启动参数，添加--no-standbox (重启后需要重新登录和   设置)

```
sudo vim /usr/share/applications/netease-cloud-music.desktop
# 将界面中Exec的值改成netease-cloud-music --no-standbox %U
```
#### deepin-wine 微信小黑框

1. 方法一：配置

要解决这个问题，你需要两个工具：`wmctrl` 和 `xdotool`：

```
sudo apt-get install wmctrl
sudo apt-get install xdotool
wmctrl -l -G -p -x
```
此时可能看到如下的输出
```
0x02e00042  0 213    0    64   1    1    wechat.exe.Wine       87a07b194048 ChatContactMenu
0x02e00044  0 213    1860 1020 60   60   wechat.exe.Wine       87a07b194048 
0x02e00041  0 213    824  422  850  617  wechat.exe.Wine       87a07b194048 微信
```
这里，只有最后一个是有用的，其他两个应该隐藏。分别执行：`xdotool windowunmap 0x02e00042`  以及  `xdotool windowunmap 0x02e00044` 完美。

2. 方法二：手动（麻烦，但是有效）
打开一个微信群聊，输入@，然后删除，解决 ...

#### 更改系统注册表

```
WINEPREFIX=~/.deepinwine/Deepin-WeChat/ deepin-wine winecfg
WINEPREFIX=~/.deepinwine/Deepin-WeChat/ deepin-wine regedit fnt.reg
WINEPREFIX=~/.deepinwine/Deepin-WeChat/ deepin-wine wineboot
```

#### 字体安装

```
# 文泉系列字体
sudo apt-get install ttf-wqy-microhei  #文泉驿-微米黑
sudo apt-get install ttf-wqy-zenhei  #文泉驿-正黑
sudo apt-get install xfonts-wqy #文泉驿-点阵宋体
```

#### 安装/卸载 .deb 文件
适用于Kubuntu系统的安装文件后缀名为 .deb，因为Kubuntu与 Debian GNU/Linux 关系密切。你可以单独的下载和安装 .deb 文件。

安装某个.deb文件，简单的在.deb文件上Right单击鼠标，然后选择Kubuntu Package Menu->安装软件包。

**安装.deb文件**
```
sudo dpkg -i 软件包名.deb
```
**卸载.deb文件**
```
sudo apt-get remove 软件包名称
```

#### 安装/卸载 .rpm 文件
**转换 .rpm 文件为 .deb 文件**

另一种安装包类型是Red Hat Package 包管理文件，以.rpm为后缀。不建议安装其到Kubuntu系统上。在大多数的情况下，都有适用于Kubuntu系统的.deb 安装包可用。然而，实在有必要的情况下，可以通过程序alien将.rpm 文件转换为.deb 文件。

1. 安装 alien 程序
2. 在终端使用管理权限运行以下命令：

```
sudo alien package_file.rpm
```
