### 版本检测

    uname -a
> uname 命令就是 Unix Name 的简写。显示机器名，操作系统和内核信息

或运行

    lsb_release -a

    cat /etc/issue

### 替换自带的更新源

    /etc/apt/sources.list

### Bash 安装目录（直接看看不到）

    C:\Users\colony\AppData\Local\lxss

### 更改默认家目录

    vim /etc/passwd

把 JACK 这个帐户对应的默认目录 `/home/JACK` 改为 `/home/JACK/code`

则每次登录时都会打开到 `code`
