---
layout: post
title: Windows下PowerShell的常用脚本以及命令设置
date: 2021-11-10
Author: DLyn
categories: 
tags: [开发环境, Windows, Terminal]
comments: true
---

#### 1、环境安装
```powershell
# 设置网络代理
netsh winhttp set proxy 127.0.0.1:1080

# 安装模块
Install-Module posh-git -Scope CurrentUser
Install-Module DirColors -Scope CurrentUser
Install-Module PSColor -Scope CurrentUser
Install-Module PSReadLine -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
```

#### 2. 在Powrshell下输入 ` $PROFILE`
```powershell
C:\Users\DLyn\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
```

#### 3. 编辑Profile文件，更新下面内容
```powershell

# 安装模块
# netsh winhttp set proxy 127.0.0.1:1080
# Install-Module posh-git -Scope CurrentUser
# Install-Module DirColors -Scope CurrentUser
# Install-Module PSColor -Scope CurrentUser
# Install-Module PSReadLine -Scope CurrentUser
# Install-Module oh-my-posh -Scope CurrentUser

# 引用和设置模块
Import-Module posh-git
Import-Module DirColors
Import-Module PSColor
Import-Module PSReadLine
Import-Module oh-my-posh
Set-PoshPrompt -Theme xtoys

# 设置预测文本来源为历史记录
Set-PSReadLineOption -PredictionSource History

# 每次回溯输入历史，光标定位于输入内容末尾
Set-PSReadLineOption -HistorySearchCursorMovesToEnd

# 设置向上键为后向搜索历史记录
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward

# 设置向下键为前向搜索历史纪录
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward

# 设置快捷键
Set-Alias ls Get-ChildItem-Wide -Option "AllScope"
Set-Alias ll Get-ChildItem
Set-Alias lla Get-ChildItem-All
Set-Alias la Get-ChildItem-All-Wide
Set-Alias clean-flutter cleanflutter
Set-Alias whereis which
Set-Alias grep findstr
Set-Alias open explorer
Set-Alias subl "D:\Sublime Text\subl.exe"

# 方法定义
function gogo {
    cd E:/Workspace/Go/src/glink
}

function current {
    cd E:/Workspace
}

function workspace {
    cd E:/Workspace
}

function library {
    cd E:/Library
}

function cleanflutter {
    flutter clean;flutter pub get
}

function setproxy {
    netsh winhttp set proxy 127.0.0.1:1080
}

function unsetproxy {
    netsh winhttp reset proxy
}

function which {
    $results =New-Object System.Collections.Generic.List[System.Object];
    foreach ($command in $args) {
        $path = (Get-Command $command).Source
        if ($path) {
            $results.Add($path);
        }
    }
    return $results;
}

function killall {
    $commands = Get-Process $args
    foreach ($command in $commands) {
        Stop-Process $command.Id
    }
}

function Get-ChildItem-Wide {
    param (
        $Path,
        $LiteralPath,
        $Filter,
        $Include,
        $Exclude,
        $Recurse,
        $Force,
        $Name,
        $UseTransaction,
        $Attributes,
        $Depth,
        $Directory,
        $File,
        $Hidden,
        $ReadOnly,
        $System
    )
    Get-ChildItem @PSBoundParameters | Format-Wide -AutoSize
}

function Get-ChildItem-All {
    param (
        $Path,
        $LiteralPath,
        $Filter,
        $Include,
        $Exclude,
        $Recurse,
        $Force,
        $Name,
        $UseTransaction,
        $Attributes,
        $Depth,
        $Directory,
        $File,
        $Hidden,
        $ReadOnly,
        $System
    )
    if ($Attributes) {
        $PSBoundParameters.Remove('Attributes');
    }
    Get-ChildItem -Attributes ReadOnly, Hidden, System, Normal, Archive, Directory, Encrypted, NotContentIndexed, Offline, ReparsePoint, SparseFile, Temporary @PSBoundParameters
}

function Get-ChildItem-All-Wide {
    param (
        $Path,
        $LiteralPath,
        $Filter,
        $Include,
        $Exclude,
        $Recurse,
        $Force,
        $Name,
        $UseTransaction,
        $Attributes,
        $Depth,
        $Directory,
        $File,
        $Hidden,
        $ReadOnly,
        $System
    )
    Get-ChildItem-All @PSBoundParameters | Format-Wide -AutoSize
}
```