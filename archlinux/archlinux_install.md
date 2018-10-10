# Installation

一、实验室主机，双硬盘，GPU: AMD/ATI Turks XT [Radeon HD 6670/7670]
> drive2 已安装 win10，在 driver1下安装 archlinux， EFI+GPT 模式安装

二、X1 yoga 2016/X1 carbon 2017 固态 单/双系统 EFI+GPT

- ## Pre-installation

    ### 联网

    + #### 无线网环境，执行以下命令，并输入连接到的 wifi 密码

            # wifi-menu

    + #### 有线网，安装前需配置 IP, DNS

        1. 查看网卡名称

                # ifconfig

        1. 设置网卡子网及 ip

                # ifconfig enp3s0 192.168.11.65 netmask 255.255.255.0

        1. 设置默认网关

                # route add default gw 192.168.11.1

        1. 设置 DNS

                # vim /etc/resolv.conf

                    nameserver 202.118.224.100

    ping 命令判断网络连接是否正常

        # ping -c 3 archlinux.org

    ### Verify the boot mode

        # ls /sys/firmware/efi/efivars

    ### Update the system clock

        # timedatectl set-ntp true

    ### Partition the disks

    1. #### efi+gpt

            # parted -l        查看磁盘状态

            # parted /dev/nvme0n1       进入分区工具
            (parted)mklabel gpt     使用gpt引导格式
            (parted)mkpart primary ext2 1 512M
            (parted)mkpart primary linux-swap 512M 8G
            (parted)mkpart primary ext4 8G 40G
            (parted)mkpart primary ext4 40G -1
            (parted)p
            (parted)q

    1. #### Format the partitions

            # mkfs.vfat -F32 /dev/nvme0n1p1
            # mkswap /dev/nvme0n1p2
            # mkfs.ext4 /dev/nvme0n1p3
            # mkfs.ext4 /dev/nvme0n1p4

    1. #### Mount the file systems

            # mount /dev/nvme0n1p3 /mnt
            # mkdir -p /mnt/boot/efi
            # mount /dev/nvme0n1p1 /mnt/boot/efi
            # mkdir -p /mnt/home
            # mount /dev/nvme0n1p4 /mnt/home
            # swapon /dev/nvme0n1p2

- ## Installation

    ### Select the mirrors

        # vim /etc/pacman.d/mirrorlist

            Server = http://mirrors.163.com/archlinux/$repo/os/$arch
            Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch
                ... 国内源 ...
    > 把列表下面的国内源转移到列表最上方

    中国大陆用户可使用以下命令选取大陆镜像服务器

        # sed -i '/China/!{n;/Server/s/^/#/};t;n' /etc/pacman.d/mirrorlist

    更新源，升级文件列表

        # pacman -Syy

    ### Install the base packages

        # pacstrap /mnt base base-devel

- ## Configure the system

    ### Generate an fstab file

        # genfstab -U /mnt >> /mnt/etc/fstab
        # cat /mnt/etc/fstab #查看文件挂载是否有错误，如无错便不需修改

    ### Change root into the new system

        # arch-chroot /mnt

    ### Time zone

        # rm /etc/localtime
        # ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

        # date
    > 检查时间是否正确

    Run hwclock(8) to generate /etc/adjtime

        # hwclock --systohc

    ### 安装无线网络驱动

        # pacman -S vim iw wpa_supplicant dialog
    > 无线环境下安装必要组件

    ### locale

        # vim /etc/locale.gen

        取消注释：
            en_US.UTF-8
            zh_CN *

    generate them with:

        # locale-gen

    Set the LANG variable in locale.conf

        # echo LANG=en_US.UTF-8 > /etc/locale.conf

    ### Hostname

        # echo luanxxys > /etc/hostname

        # vim /etc/hosts

            127.0.0.1   localhost.localdomain   localhost
            ::1     localhost.localdomain   localhost
            127.0.1.1   luanxxys.localdomain    luanxxys

    ### 安装 bootloader

    os-prober 配合 Grub 检测已经存在的系统，自动设置启动选项

        # pacman -S os-prober

        # pacman -S grub efibootmgr
        # grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub
        # grub-mkconfig -o /boot/grub/grub.cfg

    安装后检查

        # vim /boot/grub/grub.cfg

    ### Root password

        # passwd

    ### add user

        # useradd -g users -s /bin/bash -m luanxxys
        # passwd luanxxys

        # pacman -S sudo
        # chmod +w /etc/sudoers
        # vim /etc/sudoers

    在 `root ALL=(ALL)` 下面仿照格式添加自己的用户名

        # chmod -w /etc/sudoers

    ### 设置 pacman 彩色输出

        # vim /etc/pacman.conf

    找到被注释的 #Color，改为 Color。pacman就会输出彩色信息

    ### 安装驱动

        # pacman -S intel-ucode
        # pacman -S xf86-video-intel（intel 集成显卡）
        # pacman -S alsa-lib alsa-utils alsa-oss（声卡，alsa-lib 默认安装了）

    确定显卡品牌及型号

        # lspci -k | grep -A 2 -E "(VGA|3D)"

    ### 安装 Xorg

        # pacman -S xorg-server xorg-xinit

    ### 安装图形界面

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

    ### 启动图形界面前提前配置网络

        # pacman -S network-manager-applet
        # systemctl disable netctl
        # systemctl enable NetworkManager

    ### 安装字体

        # pacman -S wqy-microhei ttf-dejavu wqy-zenhei
        # fc-cache -vf
        > 搜索一下所有字体: `# pacman -Ss font`

    ### Reboot

        # exit
        # umount /mnt/boot/efi
        # umount /mnt/home
        # umount /mnt
        # reboot
    > 卸载掉 iso 文件之后 reboot

### Issue

装好系统重启后若不出现之前的系统开机启动项, 再次执行

    # pacman -S os-prober
    # grub-mkconfig -o /boot/grub/grub.cfg
