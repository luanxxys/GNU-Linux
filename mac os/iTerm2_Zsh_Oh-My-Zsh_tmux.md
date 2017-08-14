[reference](http://www.dreamxu.com/mac-terminal/)

### iTerm2

[官方网站](http://www.iterm2.com/)

hotkey|function
---|---
⌘ + Click|可以打开文件，文件夹和链接
⌘ + n|新建窗口
⌘ + t|新建标签页
⌘ + w|关闭当前页
⌘ + 数字 & ⌘ + 方向键|切换标签页
⌥⌘ + 数字|切换窗口
⌘ + enter|切换全屏
⌘ + d|左右分屏
⇧⌘ + d|上下分屏
⌘ + ;|自动补全历史记录
⇧⌘ + h|自动补全剪贴板历史
⌥⌘ + e|查找所有来定位某个标签页
⌘ + r & ⌃ + l|清屏
⌘ + /|显示光标位置
⌥⌘ + b|历史回放
⌘ + f|查找，然后用 tab 和 ⇧ + tab 可以向右和向左补全，补全之后的内容会被自动复制，还可以用 ⌥ + enter 将查找结果输入终端选中即复制，鼠标中键粘贴

hotkey|function
---|---
⌃ + u|清空当前行
⌃ + a|移动到行首
⌃ + e|移动到行尾
⌃ + f|向前移动
⌃ + b|向后移动
⌃ + p|上一条命令
⌃ + n|下一条命令
⌃ + r|搜索历史命令
⌃ + y|召回最近用命令删除的文字
⌃ + h|删除光标之前的字符
⌃ + d|删除光标所指的字符
⌃ + w|删除光标之前的单词
⌃ + k|删除从光标到行尾的内容
⌃ + t|交换光标和之前的字符

### Zsh

Mac 系统自带了 Zsh,Homebrew 来安装最新版

	brew install zsh

查看 Zsh 的版本

	zsh --version 

使用 echo $ZSH_VERSION 命令查看当前使用的 Zsh 版本

修改默认 Shell

1. 在 /etc/shells 文件中加入如下一行

		/usr/local/bin/zsh

2. 然后运行命令

		chsh -s /usr/local/bin/zsh

### Oh My Zsh

https://github.com/robbyrussell/oh-my-zsh

### Tmux

一个终端复用软件，可将终端方案化

[官方网站](http://tmux.github.io/)
