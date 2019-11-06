---
layout: post
title: Chrome插件：Vysor
date: 2019-11-04
Author: DLyn
categories: 
tags: [Extension, crack]
comments: true
---
### 手机投屏到电脑 - Chrome插件Vysor

#### 一、安装Vysor
  1、`Chrome Extension`直接搜索点击安装
  2、安装包安装
   
   安装包下载地址：`https://www.updatestar.com/directdownload/vysor/2350487`
    
   网盘地址： 链接 `https://pan.baidu.com/s/1p4YOGOKoF1iDDtTDHixOUg` 提取码 `g842`
    
#### 二、adb安装
```bash
apt-get install adb     # Ubuntu
brew install adb        # Mac
```

#### 三、adb连接
  
1、保证PC手机连接同一局域网
```bash
adb connect 192.168.2.11
```

2、 adb 无线连接不上的情况下，用数据线连接手机与电脑

3、首次连接手机上需要点击授权
```bash
adb tcpip 5555 #可重设连接端口
```

4、重复三，无线连接

5、查看连接设备状态
```bash
adb devices
```

#### 四、启动Vysor
Chrome浏览器输入 `chrome://apps` 点击图标启动 

#### 五、点击当前设备下的View按钮完成投屏


#### 六、PS:Vysor破解可解锁超清

1、查看个人文件位置 比如：`/home/glink/.config/google-chrome/Default`

```bash
chrome://version
``` 

2、点击Vysor下的Details，查看ID 比如：`hgmloofddffdnphfgcellkdfbfbjeloo`

```bash
chrome://extensions
```

3、打开Vysor的文件地址

```bash
cd /home/glink/.config/google-chrome/Default
cd Extensions
cd hgmloofddffdnphfgcellkdfbfbjeloo
```

4、目录下找到 `uglify.js` 文件，打开查找 `k="Account Management"` 然后将 `g=!1,b!=1` 改成 `g=1,b=1`

5、防止自动更新 改变版本号，找到 `manifest.json` 文件打开 更改里面版本号 （改大就行）

6、重启Vysor

7、点击当前设备下的设置按钮，选择高清dpi

参考地址：https://www.cnblogs.com/slade-sun/p/10598209.html
