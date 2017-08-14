# virtualbox 中安装 archlinux

#### 安装前联网

虚拟机中使用 NAT 方式联网，可直接借用宿主机的网络

ping 命令判断网络连接是否正常

    # ping -c 3 archlinux.org

#### Verify the boot mode

    # ls /sys/firmware/efi/efivars

#### Update the system clock

    # timedatectl set-ntp true

### Partition the disks

#### efi+gpt 模式

    # parted -l        查看磁盘状态

    # parted /dev/sda       进入分区工具
    (parted)mklabel gpt     使用gpt引导格式
    (parted)mkpart primary ext2 1 300M
    (parted)mkpart primary linux-swap 300M 6G
    (parted)mkpart primary ext4 300M -1
    (parted)p
    (parted)q

    # parted -l

#### Format the partitions

    # mkfs.vfat -F32 /dev/sda1
    # mkswap /dev/sda2
    # mkfs.ext4 /dev/sda3

#### Mount the file systems

    # mount /dev/sda3 /mnt
    # mkdir -p /mnt/boot
    # mount /dev/sda1 /mnt/boot
    # swapon /dev/sda2

#### Select the mirrors

    # vim /etc/pacman.d/mirrorlist

添加

    Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch
    Server = http://mirrors.163.com/archlinux/$repo/os/$arch
    Server = http://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
    Server = http://mirrors.zju.edu.cn/archlinux/$repo/os/$arch

> 其中的浙大源在文件中，记得注释掉（vim 剪切到上面）

然后更新源，升级文件列表

    # pacman -Syy

#### Install the base packages

    # pacstrap /mnt base base-devel

> 若出现 error:failed to install packages to new root

    # pacman -Scc   清理所有的缓存文件

#### Generate an fstab file

    # genfstab -U /mnt >> /mnt/etc/fstab
    # cat /mnt/etc/fstab #查看文件挂载是否有错误，如无错便不需修改

#### Change root into the new system:

    # arch-chroot /mnt

#### Time zone

Set the time zone:

        # rm /etc/localtime
        # ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

Run hwclock(8) to generate /etc/adjtime:
    
    # hwclock --systohc
> This command assumes the hardware clock is set to UTC

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

#### 安装 bootloader

    # pacman -S grub-efi-x86_64 efibootmgr
    # grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=boot
    # grub-mkconfig -o /boot/grub/grub.cfg

vbox对efi的模拟只能运行在uefi固件上，还不够完善，所以只认bootx64.efi这个名字

    # mv /boot/EFI/boot/grubx64.efi /boot/EFI/boot/bootx64.efi

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

#### 安装Xorg

    sudo pacman -S xorg-server xorg-xinit

在安装好了x以及x那一揽子组件之后，这次新版本的驱动似乎把vboxvideo给移除了，所以还需要手动安装vboxvideo等驱动程序

    $ sudo pacman virtualbox-guest-utils

重启或手动加载模块，才能执行下一条语句

    $ sudo VBoxClient-all
> reboot 后生效

    startx
        成功一闪而过

#### 安装桌面管理器

    sudo pacman -S gdm

设置开机启动 gdm 服务

    sudo systemctl enable gdm

gdm背景：输入以下指令

    curl -L -O http://archibold.io/sh/archibold
    chmod +x archibold
    ./archibold login-backgroung <bg_path>

重启后gdm就会变成你要的背景

##### 安装图形界面

安装i3窗口管理器

    sudo pacman -S i3

安装Gnome

    sudo pacman -S gnome

##### 重启前配置网络

    sudo pacman -S network-manager-applet
    sudo systemctl disable netctl
    sudo systemctl enable NetworkManager

### 安装字体

首先使用pacman搜索一下所有字体，然后安装所需的字体：

    # pacman -Ss font

安装文泉微米黑

    # pacman -S wqy-microhei

##### 设置pacman彩色输出

打开/etc/pacman.conf文件，找到被注释的#Color，改为Color。pacman就会输出彩色信息，方便查看
