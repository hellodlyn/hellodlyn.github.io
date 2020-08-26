---
layout: post
title: VUE SEO Phantomjs
date: 2020-06-05
Author: DLyn
categories: 
tags: [vue, seo]
comments: true
---

#### 安装phantomjs
**Ubuntu**
```bash
sudo apt-get install phantomjs
```
**Centos：**

```bash
# 下载安装包
wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
# 安装bzip2
yum install bzip2
# 解压安装包
tar -jxvf phantomjs-2.1.1-linux-x86_64.tar.bz2
# 移动安装包位置
mv phantomjs-2.1.1-linux-x86_64 /usr/local/src/phantomjs
# 创建命令链接
ln -sf /usr/local/src/phantomjs/bin/phantomjs /usr/local/bin/phantomjs

# 测试版本号
phantomjs -v 
```

![image-20200715180002260](/home/glink/Workspace/Doc/image-20200715180002260.png)