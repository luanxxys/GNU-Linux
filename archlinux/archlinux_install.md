# 记录安装过程
> X1 yoga 硬盘 EFI+GPT 模式安装

## Pre-installation

#### 联网

如果你是有线网并且路由器支持DHCP的话插上网线后先执行以下命令获取IP地址：

    # systemctl enable dhcpcd

如果你是无线网，请执行以下命令：

    wifi-menu

ping 命令判断网络连接是否正常

    # ping -c 3 archlinux.org

#### Verify the boot mode

    # ls /sys/firmware/efi/efivars

#### Update the system clock

    # timedatectl set-ntp true

### Partition the disks

#### efi+gpt 模式

    parted -l        查看磁盘状态

    # parted /dev/sda       进入分区工具
    (parted)mklabel gpt     使用gpt引导格式
    (parted)mkpart primary ext2 1 300M
    (parted)mkpart primary linux-swap 300M 8G
    (parted)mkpart primary ext4 300M -1
    (parted)p
    (parted)q

    parted -l

#### Format the partitions

    # mkfs.vfat -F32 /dev/sda1
    # mkswap /dev/sda2
    # mkfs.ext4 /dev/sda3

#### Mount the file systems

    # mount /dev/sda3 /mnt
    # mkdir -p /mnt/boot/efi
    # mount /dev/sda1 /mnt/boot/efi
    # swapon /dev/sda2

## Installation

#### Select the mirrors

    #vim /etc/pacman.d/mirrorlist

添加

    Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch
    Server = http://mirrors.163.com/archlinux/$repo/os/$arch
    Server = http://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
    Server = http://mirrors.zju.edu.cn/archlinux/$repo/os/$arch
> 把列表下面的浙大源注释掉

然后更新源，升级文件列表

    # pacman -Syy

#### Install the base packages

    # pacstrap /mnt base base-devel

## Configure the system

#### Generate an fstab file

    # genfstab -U /mnt >> /mnt/etc/fstab
    # cat /mnt/etc/fstab #查看文件挂载是否有错误，如无错便不需修改

#### Change root into the new system:

    # arch-chroot /mnt

#### Time zone

Set the time zone:

    # rm /etc/localtime
    # ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

    # date
> 检查时间是否正确

Run hwclock(8) to generate /etc/adjtime:

    # hwclock --systohc

#### 安装网络驱动

    # pacman -S vim iw wpa_supplicant dialog
> 无线环境下安装必要组件

#### Locale

    # vim /etc/locale.gen

取消注释：

    en_US.UTF-8
    zh_CN.UTF-8
    zh_CN.GBK
    zh_CN.GB2312

generate them with:

    # locale-gen

Set the LANG variable in locale.conf

    # echo LANG=en_US.UTF-8 > /etc/locale.conf

#### Hostname

    # echo arch_luanxxy > /etc/hostname

    # vim /etc/hosts

修改如下

    127.0.0.1	localhost.localdomain	localhost
    ::1		localhost.localdomain	localhost
    127.0.1.1	arch_luanxxy.localdomain	arch_luanxxy

#### Root password

    # passwd

#### 安装Intel-ucode

    # pacman -S intel-ucode

#### 安装 bootloader

    # pacman -S grub-efi-x86_64 efibootmgr
    # grub-install --efi-directory=/boot/efi --bootloader-id=grub
    # grub-mkconfig -o /boot/grub/grub.cfg

安装后检查

    # vim /boot/grub/grub.cfg

#### Reboot

    # exit
    # umount /mnt/boot
    # umount /mnt
    # reboot
> 卸载掉 iso 文件之后 reboot

#### add user

    # useradd -g users -s /bin/bash -m luanxxy
    # passwd luanxxy

    # pacman -S sudo
    # vim /etc/sudoers
> 在 root ALL=(ALL)下面仿照格式添加自己的用户名

####重启之后可能上不了网- --> wait  a moment

无线

    wifi-menu

有线
    
    dhcpcd

#### 设置pacman彩色输出

打开/etc/pacman.conf文件，找到被注释的#Color，改为Color。pacman就会输出彩色信息，方便查看

#### 安装显卡（intel 集成显卡）

    sudo pacman -S xf86-video-intel

#### 安装Xorg

    sudo pacman -S xorg-server xorg-xinit

#### 安装桌面管理器

    sudo pacman -S gdm

设置开机启动 gdm 服务

    sudo systemctl enable gdm

设置gdm背景，输入以下指令

    curl -L -O http://archibold.io/sh/archibold
    chmod +x archibold
    ./archibold login-backgroung 你的背景的地址

重启后gdm就会变成你要的背景

#### 安装图形界面

安装i3窗口管理器

    sudo pacman -S i3

安装Gnome

    sudo pacman -S gnome
> 各图形界面下，只有 gnome 环境下 chrome 能直接使用 lantern

安装Xfce

    sudo pacman -S xfce4

#### 启动图形界面前提前配置网络

    sudo pacman -S network-manager-applet
    sudo systemctl disable netctl
    sudo systemctl enable NetworkManager


