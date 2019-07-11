---
layout: post
title: GIT 常用设置
date: 2019-07-11
Author: DLyn
categories: 
tags: [git, 开发环境]
comments: true
---

git配置文件位置  ·/.gitconfig

```
[credential]
    helper = store
[alias]
    tree = log --all --graph --decorate --abbrev-commit --color --date=short --pretty=format:'%C(auto)%h%Creset -%C(auto)%d%Creset %s %C(bold blue)[%an | %ad]%Creset'
[color]
	ui = auto
```
