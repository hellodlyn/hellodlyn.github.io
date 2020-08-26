---
layout: post
title: pip安装python库问题记录
date: 2020-06-05
Author: DLyn
categories: 
tags: [pip, python]
comments: true
---

1. pip install pyautogui 安装失败

**报出错误：**
```
...
AttributeError: module 'enum' has no attribute 'IntFlag'
----------------------------------------
```
**解决办法：**
```
pip uninstall -y enum34
```
