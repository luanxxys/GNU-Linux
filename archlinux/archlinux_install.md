# 记录安装过程
> 一、实验室主机，双硬盘，GPU: AMD/ATI Turks XT [Radeon HD 6670/7670]
>
> drive2 已安装 win10，在 driver1下安装 archlinux， EFI+GPT 模式安装

> 二、X1 yoga 2016/X1 carbon 2017 固态 单系统 EFI+GPT

- ## Pre-installation

    #### 联网

    + 有线网，安装前需配置 IP、DNS

        查看网卡名称

            # ifconfig

        设置网卡子网及 ipfc-cache -vf

            # ifconfig enp3s0 192.168.11.65 netmask 255.255.255.0

        设置默认网关

            # route add default gw 192.168.11.1

        设置 DNS

            # vim /etc/resolv.conf

            nameserver 202.118.224.100

    + 无线网环境，执行以下命令，并输入连接到的 wifi 密码

            # wifi-menu

    ping 命令判断网络连接是否正常

        # ping -c 3 archlinux.org

    #### Verify the boot mode

        # ls /sys/firmware/efi/efivars

    #### Update the system clock

        # timedatectl set-ntp true

    #### Partition the disks

    ##### efi+gpt 模式

        # parted -l        查看磁盘状态

        # parted /dev/nvme0n1p       进入分区工具
        (parted)mklabel gpt     使用gpt引导格式
        (parted)mkpart primary ext2 1 300M
        (parted)mkpart primary linux-swap 300M 8G
        (parted)mkpart primary ext4 8G -1
        (parted)p
        (parted)q

    ##### Format the partitions

        # mkfs.vfat -F32 /dev/nvme0n1p1
        # mkswap /dev/nvme0n1p2
        # mkfs.ext4 /dev/nvme0n1p3

    ##### Mount the file systems

        # mount /dev/nvme0n1p3 /mnt
        # mkdir -p /mnt/boot/efi
        # mount /dev/nvme0n1p1 /mnt/boot/efi
        # swapon /dev/nvme0n1p2

- ## Installation

    #### Select the mirrors

        # vim /etc/pacman.d/mirrorlist

    添加

        Server = http://mirrors.163.com/archlinux/$repo/os/$arch
        Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch
            ... 国内源 ...
    > 把列表下面的国内源转移到列表最上方

    然后更新源，升级文件列表

        # pacman -Syy

    #### Install the base packages

        # pacstrap /mnt base base-devel

- ## Configure the system

    #### Generate an fstab file

        # genfstab -U /mnt >> /mnt/etc/fstab
        # cat /mnt/etc/fstab #查看文件挂载是否有错误，如无错便不需修改

    #### Change root into the new system

        # arch-chroot /mnt

    #### Time zone

        # rm /etc/localtime
        # ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

        # date
    > 检查时间是否正确

    Run hwclock(8) to generate /etc/adjtime

        # hwclock --systohc

    #### 安装无线网络驱动

        # pacman -S vim iw wpa_supplicant dialog
    > 无线环境下安装必要组件

    #### locale

        # vim /etc/locale.gen

    取消注释：

        en_US.UTF-8
        zh_CN *

    generate them with:

        # locale-gen

    Set the LANG variable in locale.conf

        # echo LANG=en_US.UTF-8 > /etc/locale.conf

    #### Hostname

        # echo arch_luanxxys > /etc/hostname

        # vim /etc/hosts

    修改如下

        127.0.0.1   localhost.localdomain   localhost
        ::1     localhost.localdomain   localhost
        127.0.1.1   arch_luanxxys.localdomain    arch_luanxxys

    #### 安装 bootloader

        # pacman -S grub-efi-x86_64 efibootmgr
        # grub-install --efi-directory=/boot/efi --bootloader-id=grub
        # grub-mkconfig -o /boot/grub/grub.cfg

    安装后检查

        # vim /boot/grub/grub.cfg

    #### Root password

    登陆 root 账号，设置密码

        # passwd

    #### add user

        # useradd -g users -s /bin/bash -m luanxxys
        # passwd luanxxys

        # pacman -S sudo
        # chmod +w /etc/sudoers
        # vim /etc/sudoers
    > 在 root ALL=(ALL)下面仿照格式添加自己的用户名

        # chmod -w /etc/sudoers

    #### 设置 pacman 彩色输出

            # vim /etc/pacman.conf

    找到被注释的 #Color，改为 Color。pacman就会输出彩色信息

    #### 安装 Xorg

        # pacman -S xorg-server xorg-xinit

    #### 安装图形界面

    安装 gnome

        # pacman -S gnome

    设置开机启动 gdm 服务
    > 若安装 gnome，则不用单独安装 gdm

        # systemctl enable gdm

    设置 gdm 背景，输入以下指令

        curl -L -O http://archibold.io/sh/archibold
        chmod +x archibold
        ./archibold login-backgroung 你的背景的地址
    > 重启后gdm就会变成你要的背景

    安装 i3 窗口管理器

        sudo pacman -S i3

    #### 启动图形界面前提前配置网络

        # pacman -S network-manager-applet
        # systemctl disable netctl
        # systemctl enable NetworkManager

    #### 安装驱动

        # pacman -S intel-ucode
        # pacman -S xf86-video-intel（intel 集成显卡）
        # pacman -S alsa-lib alsa-utils alsa-oss（声卡，alsa-lib 默认安装了）
        # pacman -S xf86-input-synaptics（触摸板）
        # yaourt thinkfan
            #　systemctl enable thinkfan.service
            风扇控制， /etc/thinkfan.conf，修改最后的几行数字。语法：(Level, Low, High

        # yaourt -S fingerprint-gui（指纹识别）
            当前用户添加到plugdev和scanner组中
                # usermod -a -G plugdev,scanner luanxxys
            在/etc/pam.d/中的su,sudo,login,gdm等文件里添加
                auth       required pam_env.so
                auth       sufficient   pam_fingerprint-gui.so
                auth       sufficient   pam_unix.so try_first_pass likeauth nullok
                auth       required pam_deny.so

    #### 安装字体

    文泉微米黑

        # pacman -S ttf-bitstream-vera ttf-dejavu ttf-droid wqy-microhei
        # yaourt ttf-ms-fonts
        # fc-cache -vf
        > 搜索一下所有字体: `# pacman -Ss font`

    #### Reboot

        # exit
        # umount /mnt/boot/efi
        # umount /mnt
        # reboot
    > 卸载掉 iso 文件之后 reboot

    #### 安装 AMD 显卡驱动

    查看显卡信息

        lspci | grep VGA

    查看显卡状态

        # cat /sys/kernel/debug/vgaswitcheroo/switch
    > 不一定显示有这个文件夹

    安装

        yaourt catalyst
    > 暂未成功

### 安装效果

双硬盘台式机开机默认启动 Arch Linux，且无 win10 启动项。开机 F12，可选择 Windows boot
