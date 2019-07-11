---
layout: post
title: Linux搜狗输入法候选词乱码
date: 2019-07-11
Author: DLyn
categories: 
tags: [开发环境, linux, 输入法]
comments: true
---

输入如下命令：

```
cd ~/.config
sudo rm -rf SogouPY* sogou*
```

然后注销即可(注意，这里必须是注销，不注销直接重启并不管用)