# After installation

### 安装 yaourt

    sudo vim /etc/pacman.conf

将下面这三行加入到文件末尾并保存

    [archlinuxcn]
    SigLevel = Never
    Server = http://repo.archlinuxcn.org/$arch

同步软件信息库并安装 yaourt

    sudo pacman -Sy yaourt fakeroot

导入GPG Key，否则 Yaourt 安装软件会报错

    sudo pacman -S archlinuxcn-keyring

查找有关 ambiance 的软件包

    yaourt ambiance

要安装你需要的软件包，只要输入这个软件包的序数

滚动更新命令使用 yaourt

    yaourt -Syu --aur

其它功能及操作

    $ yaourt -Sdd <package_name>  # 跳过所有依赖检查，并安装 <package_name>
    $ yaourt -Qi <package_name>   # 查询软件包信息/依赖，如本机缺少相关依赖，使用 dnf 进行安装
    $ yaourt-link -s <package_name>  # 将隔离环境中的包软链接至系统删除 <package_name>
    $ yaourt-link -r <package_name>  # 删除系统中的软链接
    $ yaourt -R <package_name>   # 删除 <package_name>
    $ yaourt -Q   # 查询已安装软件包
    $ yaourt -Qdt   # 删除全部孤立无用软件包

### 安装驱动

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

> 安装 fingerprint-gui 后，提示找不到指纹设备（x1 yoga 2016）

### [软件](https://github.com/luanxxys/env/software)

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
    ...
