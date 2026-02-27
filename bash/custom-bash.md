## Linux bashrc常用配置内容

`.bashrc`是Bash shell的用户级配置文件，每次打开新终端时都会被执行。以下是常用的配置项：

### 1. PATH环境变量设置
```bash
# 添加自定义软件路径到PATH
export PATH="$HOME/bin:$HOME/.local/bin:$PATH"
export PATH="/usr/local/bin:$PATH"
```

### 2. 常用别名(Alias)
```bash
# 基础命令别名
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias ls='ls --color=auto'
alias cls='clear'
alias grep='grep --color=auto'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'

# 安全操作
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# 目录操作
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
alias ~='cd ~'

# Git相关
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git log'

# 快速跳转
alias www='cd /var/www/html'
alias logs='cd /var/log'
```

### 3. 自定义提示符(PS1)
```bash
# 基础提示符
export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '

# 带颜色和时间的复杂提示符
export PS1='\[\033[32;1m\]\u \[\033[33;1m\]\t \[\033[35;1m\]\w \n\[\033[0;0m\]$ '
```

### 4. 历史记录配置
```bash
# 增加历史记录条目数
export HISTSIZE=5000
export HISTFILESIZE=10000

# 为历史记录添加时间戳
export HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S "

# 避免记录重复命令
export HISTCONTROL=ignoredups:erasedups

# 追加历史记录而不是覆盖
shopt -s histappend
```

### 5. 自动补全和shell选项
```bash
# 启用bash补全
if [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
fi

# 设置补全忽略大小写
bind "set completion-ignore-case on"

# 其他有用的shell选项
shopt -s cdspell        # 自动纠正cd拼写错误
shopt -s checkwinsize    # 检查窗口大小变化后重绘
```

### 6. 自定义函数
```bash
# 创建目录并立即进入
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# 查看目录大小
dus() {
    du -sh "$@" | sort -h
}

# 查找进程
psgrep() {
    ps aux | grep "$1" | grep -v grep
}
```

### 7. 编辑器和其他环境变量
```bash
# 设置默认编辑器
export EDITOR=vim
export VISUAL=vim

# 语言环境设置
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8

# 设置umask
umask 022
```

### 8. 欢迎消息(可选)
```bash
# 显示欢迎消息
echo "Welcome back, $USER! Today is $(date)"
```

### 配置生效方法
修改后需要执行以下命令使配置立即生效：
```bash
source ~/.bashrc
# 或者
. ~/.bashrc
```

### 备份和恢复技巧
- 修改前先备份：`cp ~/.bashrc ~/.bashrc.backup`
- 如果需要恢复默认配置：`cp /etc/skel/.bashrc ~/.bashrc`

这些配置能大幅提升Linux命令行使用体验，您可以根据自己的需求选择性地添加到`~/.bashrc`文件中。
