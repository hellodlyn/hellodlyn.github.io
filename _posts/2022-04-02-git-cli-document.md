---
layout: post
title: Git 命令行使用说明
date: 2022-04-02
Author: DLyn
categories: 
tags: [git, software]
comments: true
---
## 名词解释

**Workspace**：工作区
**Stage/Index**：暂存区
**Repository**:本地仓库
**Remote**：远端仓库

<img src="https://glink-assets.oss-cn-beijing.aliyuncs.com/images/docs/bg2015120901-20220322154238156.png" alt="img" style="zoom:67%;" />

## 常用命令

**git clone**

```bash
# 拉取代码
# -b 指定分支(默认master)
# -depth 指定拉取深度(默认全部)
# ./GitPushTest 本地仓库存储地址(不填写，默认仓库名git-push-test)
git clone https://aa.bb.cc/dlyn/git-push-test.git -b master --depth=1 ./GitPushTest
```

**git pull**

```bash
# 拉取远端代码
git pull origin master
```

**git add**

```bash
# 添加到暂存区
git add . 
```

**git commit** 

```bash
# 提交修改
git commit -m '这是提交的日志'
```

**git push** 

```bash
# 推送指定分支
git push origin master
```

**git fetch**

```bash
# 同步远端代码到本地
git fetch --all
```

**Branch - 分支**

```bash
# 创建分支
git branch test
 
# 创建新分支并切换
git switch -c test2
git checkout -b test3

# 切换分支
git checkout test2
git switch test3

# 推送分支到远端
git push origin test

# 删除本地分支(不能删除当前分支)
git branch -d test

# 删除远端分支
git push origin --delete test
```

**Tag - 标签**

```bash
# 创建TAG
git tag -a v2.0.0 -m '添加新功能'

# 推送TAG到远端
git push origin v2.0.0

# 删除TAG
git tag -d v2.0.0

# 删除远端TAG
git push origin :refs/tags/test.v.1.0
```

## 其他命令

**git reset**:退回指定的提交(针对当前分支)

**git restore** / **git checkout**：撤回文件(针对文件)

  ```bash
# 撤销当前工作区文件修改
git restore

# 将文件从缓存区撤回到工作区
git restore --staged
git checkout -- 
  ```

**git switch** / **git checkout**：切换分支

```bash
# 切换到分支
git switch master 
git checkout master 

# 创建新的分支，并切换
git switch -c master2
git checkout -b master2
```

**git stash**：暂存当前工作区的内容

```bash
# 保存当前工作区
git stash

# 显示已经保存的内容
git stash list

# 取回保存的内容
git stash apply --index

# 取回保存的内容
git stash pop --index

# 丢弃保存的内容(指定ID)
git stash drop --index

# 丢弃所有保存
git stash clear
```

**git merge**

生成一个节点，合并分支（将两个分支线“接”到一起，生成一个“结”）

**git rebase** 

将当前分支的Base点，重新定位

**git cherry-pick** 

将某一条提交“摘”出来，“安”在当前的分支上面

## 情景说明

1、Git怎么记住密码

- SSH秘钥配置
- 修改.gitconfig，保存密码

2、提交的时候，Log写错了，怎么修改Log

```
git commit --amend
```

3、版本提交错了，怎么回到指定版本

**git reset --hard** 强制将分支重置到之前版本

<img src="https://glink-assets.oss-cn-beijing.aliyuncs.com/images/docs/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwNDE0MjEyMjIxMDMz-20220322154229321.png" alt="img" style="zoom: 67%;" />

PS: reset之后，push到云端的时候会有限制

**git revent** 创建一个新的提交，将所有的文件修改到指定版本

<img src="https://glink-assets.oss-cn-beijing.aliyuncs.com//images/docs/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwNDE0MjA1ODE2MTg4.png" alt="img" style="zoom: 67%;" />

4、新版本开发到一半，如何修改上一个版本的bug

5、同一个仓库，如何关联两个Git地址

```bash
git remote add origin2 https://a.bb.cc/test.git
```

6、clone的时候使用了，depth参数后，怎么恢复

```bash
git fetch --unshadow
```

## 其他

**git submodule**：关联当前项目与子模块

```bash
# 添加submodule
git submodule add https://aa.bb.cc/test.git module

# 手动初始化包含子模块的项目
git clone https://aa.bb.cc/test-submodule.git .
git submodule init 
git submodule update

# 递归克隆整个项目，有子模块同步更新，一步到位。
git clone https://aa.bb.cc/test.git assets --recursive 


# 删除子模块
# 1. 删除子模块文件夹
git rm --cached module
rm -rf module

# 2. 删除.gitmodules文件中相关子模块信息
[submodule "module"]
  path = module
  url = https://aa.bb.cc/test.git

# 3. 删除.git/config中的相关子模块信息
[submodule "module"]
  url = https://aa.bb.cc/test.git

# 4. 删除.git文件夹中的相关子模块文件
rm -rf .git/modules/module
```

**git lfs**：Git的扩展，用于实现 Git 对大文件的支持，减少主库的数据量

```bash
# 开启lfs功能
git lfs install 

# 命令进行大文件追踪,生成或者更新 .gitattributes 文件
git lfs track "*.so"

# 查看现有的追踪模式
git lfs track

# 可以显示当前跟踪的文件列表
git lfs ls-files

# 拉取带lfs的项目
git clone
git lfs clone
```

## 附录

**.gitconfig**

```
[credential]
    helper = store
[alias]
    tree = log --graph --decorate --abbrev-commit --color --date=short --pretty=format:'%C(auto)%h%Creset -%C(auto)%d%Creset %s %C(bold blue)[%an | %ad]%Creset'
[color]
    ui = auto
[http]
    # proxy = http://127.0.0.1:1081
    postBuffer = 524288000
[https]
    # proxy = http://127.0.0.1:1081
    postBuffer = 524288000
[core]
    compression = -1
    quotepath = false
[filter "lfs"]
    required = true
    clean = git-lfs clean -- %f
    smudge = git-lfs smudge -- %f
    process = git-lfs filter-process
[init]
	  defaultBranch = master
```