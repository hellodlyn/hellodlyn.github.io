---
layout: post
title: 树莓派 Raspbian 开发环境设置
date: 2019-09-18
Author: DLyn
categories: 
tags: [开发环境, 树莓派, 镜像/代理]
comments: true
---
#### 树莓派 Raspbian 安装 Python3 的 PyQt5 运行环境
树莓派`Raspbian`下使用 `pip3 install PyQt5` 无法正常安装，但其实官方apt已经提供了更简单的安装包。
```bash
sudo apt install -y python3-pyqt5
```
执行上述命令，即可安装PyQt5。但这个库默认不包含QtWebkit之类的组件，需要额外安装。所有额外组件一起安装，执行命令：
```bash
sudo apt install -y python3-pyqt5.qsci python3-pyqt5.qtmultimedia python3-pyqt5.qtopengl python3-pyqt5.qtpositioning python3-pyqt5.qtquick python3-pyqt5.qtsensors python3-pyqt5.qtserialport python3-pyqt5.qtsql python3-pyqt5.qtsvg python3-pyqt5.qtwebchannel python3-pyqt5.qtwebkit python3-pyqt5.qtwebsockets python3-pyqt5.qtx11extras python3-pyqt5.qtxmlpatterns
```

#### Raspbian软件源镜像-清华大学
Debian 7 (wheezy)
```bash
# 编辑 `/etc/apt/sources.list` 文件，删除原文件所有内容，用以下内容取代：
deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ wheezy main non-free contrib
deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ wheezy main non-free contrib

# 编辑 `/etc/apt/sources.list.d/raspi.list` 文件，删除原文件所有内容，用以下内容取代：
deb http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ wheezy main ui
```
Debian 8 (jessie)
```bash
# 编辑 `/etc/apt/sources.list` 文件，删除原文件所有内容，用以下内容取代：
deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ jessie main non-free contrib
deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ jessie main non-free contrib

# 编辑 `/etc/apt/sources.list.d/raspi.list` 文件，删除原文件所有内容，用以下内容取代：
deb http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ jessie main ui
```
Debian 9 (stretch)
```bash
# 编辑 `/etc/apt/sources.list` 文件，删除原文件所有内容，用以下内容取代：
deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ stretch main non-free contrib
deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ stretch main non-free contrib

# 编辑 `/etc/apt/sources.list.d/raspi.list` 文件，删除原文件所有内容，用以下内容取代：
deb http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ stretch main ui
```
Debian 10 (buster)
```bash
# 编辑 `/etc/apt/sources.list` 文件，删除原文件所有内容，用以下内容取代：
deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main non-free contrib
deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main non-free contrib

# 编辑 `/etc/apt/sources.list.d/raspi.list` 文件，删除原文件所有内容，用以下内容取代：
deb http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui
```
注意：网址末尾的 `raspbian` 重复两次是必须的。因为Raspbian的仓库中除了APT软件源还包含其他代码。APT软件源不在仓库的根目录，而在 `raspbian/` 子目录下。

编辑镜像站后，请使用 `sudo apt-get update` 命令，更新软件源列表，同时检查您的编辑是否正确。

> 原文地址 : <https://mirror.tuna.tsinghua.edu.cn/help/raspbian/>
