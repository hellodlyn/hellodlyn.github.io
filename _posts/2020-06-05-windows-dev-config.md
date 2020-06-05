---
layout: post
title: Windows开发环境设置配置
date: 2020-06-05
Author: DLyn
categories: 
tags: [windows, 开发环境]
comments: true
---

#### Git Bash 默认样式修改
**Bash命令行展示信息**
打开文件：`Git安装路径/etc/profile.d/git-prompt.sh`,修改下面配置
```bash
if test -f ~/.config/git/git-prompt.sh
then
	. ~/.config/git/git-prompt.sh
else
	PS1='\[\033]0;$TITLEPREFIX:$PWD\007\]' # set window title
	# PS1="$PS1"'\n'                 # new line
	PS1="$PS1"'\[\033[32m\]'       # change to green
	PS1="$PS1"'\u@\h'             # user@host<space>
	PS1="$PS1"'\[\033[0m\]'        # change color
	PS1="$PS1"':'             # :
	# PS1="$PS1"'\[\033[35m\]'       # change to purple
	# PS1="$PS1"'$MSYSTEM '          # show MSYSTEM
	PS1="$PS1"'\[\033[33m\]'       # change to brownish yellow
	PS1="$PS1"'\W'                 # current working directory
	if test -z "$WINELOADERNOEXEC"
	then
		GIT_EXEC_PATH="$(git --exec-path 2>/dev/null)"
		COMPLETION_PATH="${GIT_EXEC_PATH%/libexec/git-core}"
		COMPLETION_PATH="${COMPLETION_PATH%/lib/git-core}"
		COMPLETION_PATH="$COMPLETION_PATH/share/git/completion"
		if test -f "$COMPLETION_PATH/git-prompt.sh"
		then
			. "$COMPLETION_PATH/git-completion.bash"
			. "$COMPLETION_PATH/git-prompt.sh"
			PS1="$PS1"'\[\033[36m\]'  # change color to cyan
			PS1="$PS1"'`__git_ps1`'   # bash function
		fi
	fi
	PS1="$PS1"'\[\033[0m\]'        # change color
	# PS1="$PS1"'\n'                 # new line
	PS1="$PS1"'$ '                 # prompt: always $
fi
```

