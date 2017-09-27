# Fedora 26 安装使用
> 最开始 U盘 安装 Fedora 26，但因为因为各种软件源不可用，便重新安装 Fedora 25,使用升级的方式更新到 Fedora 26
>
> 在 win 10 下使用 rufus 制作启动盘

- ### 添加源    

        # cd /etc/yum.repos.d

    * #### 安装RPMFusion源：

            # rpm -ivh http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm
            # rpm -ivh http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm

    * #### 安装FZUG源（中文Fedora社区的软件源）：

            # dnf config-manager --add-repo=http://repo.fdzh.org/FZUG/FZUG.repo

    * #### 163源(添加到当前目录下)

            # wget http://mirrors.163.com/.help/fedora-163.repo
            # wget http://mirrors.163.com/.help/fedora-updates-163.repo

    安装好了源之后，使用命令

        # dnf makecache

    将服务器上的软件包信息在本地进行缓存，以提高搜索和安装软件的速度

        sudo dnf clean all && sudo dnf autoremove

        sudo dnf update && sudo dnf upgrade

- ### 各种应用程序

    [参考](https://github.com/luanxxys/software)

- ### Issue

    + #### Enabling DNF’s Fastest Mirror Plugin

        I’ve found that the fastestmirror plugin helps reduce times for downloads and updates, so enabling it is the first thing that I do.  Use the editor of your choice for the below – my example uses gedit, since it’s already installed by default.

            sudo vim /etc/dnf/dnf.conf

        Add the below line to the bottom of the file, then you’re done.

            fastestmirror=true

        Save and exit the file

    + #### Adobe Flash Player 26 on Fedora 26/25()

    [reference](https://www.if-not-true-then-false.com/2010/install-adobe-flash-player-10-on-fedora-centos-red-hat-rhel/)

        * ##### Adobe Repository 64-bit x86_64

                # rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm
                # rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux

        * ##### Fedora 26/25/24

                # dnf install flash-plugin alsa-plugins-pulseaudio libcurl

- ### 待办

        xmind
        fingerprint driver
