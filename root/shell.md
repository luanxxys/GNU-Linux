### 安装了的shell

    chsh -l

或

    cat /etc/shells

### 查看当前正在使用的shell

    $ echo $SHELL


### 改变当前的shell

    $ chsh -s /bin/zsh

    -s 修改登录的shell

现在执行 'echo $SHELL' 后仍然输出为/bin/bash，这是因为你需要重启你的shell才完全切换到 zsh

> chsh -s 其实修改的就是/etc/passwd文件里和你的用户名相对应的那一行
