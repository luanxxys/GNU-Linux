### 安装yaourt

以root权限打开编译/etc/pacman.conf，将下面这三行加入到文件末尾并保存：

    [archlinuxcn]
    SigLevel = Never
    Server   =  http://repo.archlinuxcn.org/$arch

同步软件信息库并安装yaourt

    sudo pacman -Sy yaourt fakeroot

导入GPG Key，否则Yaourt安装软件会报错

    pacman -S archlinuxcn-keyring

查找有关ambiance的软件包

    yaourt ambiance

要安装你需要的软件包，只要输入这个软件包的序数

滚动更新命令使用yaourt

    yaourt -Syu --aur

其它功能及操作

    $ yaourt -Sdd ppsspp  # 跳过所有依赖检查，并安装 ppsspp
    $ yaourt -Qi ppsspp   # 查询软件包信息/依赖，如本机缺少相关依赖，使用 dnf 进行安装
    $ yaourt-link -s ppsspp  # 将隔离环境中的包软链接至系统删除 ppsspp
    $ yaourt-link -r ppsspp  # 删除系统中的软链接
    $ yaourt -R ppsspp   # 删除 ppsspp
    $ yaourt -Q   # 查询已安装软件包

### 安装字体

首先使用pacman搜索一下所有字体，然后安装所需的字体：

    # pacman -Ss font

安装文泉微米黑

    # pacman -S wqy-microhei

## 软件

libreoffice pycharm virtualbox netease-cloud-music
qBittorrent tor-browser guke-terminal ntfs-3g
git openssh zip rar p7zip unzip unrar zeal
google-chrome lantern fbreader wireshark
xmind albert gnome-shell-pomodoro

#### 待尝试

thefuck tmux  
chmsee-查看chm文件

### [fcitx](github.com/luanxxys/software/fcitx)

#### zsh 美化

    安装完成之后打开.zshrc文件配置。我喜欢将主题设置为random，启用几个插件，并添加vim的简化命令。

    ZSH_THEME="random"

    plugins=(git archlinux history mvn python git-extras textmate lighthouse autojump)

    # Example aliases
    alias zshconfig="mate ~/.zshrc"
    alias ohmyzsh="mate ~/.oh-my-zsh"
    alias vi=vim

### arch-chroot 修复系统

U盘启动进入 livecd 的环境

挂在原系统

    mount /dev/sda3 /mnt
    ...

进入系统

    arch-chroot /mnt

进行修复

    pacman -S udev 
    pacman -S mkinitcpio
    mkinincpio -p linux