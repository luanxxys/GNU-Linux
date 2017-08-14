# Fedora 26 安装使用
> 最开始 U盘 安装 Fedora 26，但因为因为各种软件源不可用，便重新安装 Fedora 25,使用升级的方式更新到 Fedora 26
>
> 在 win 10 下使用 rufus 制作启动盘

- ### 添加源    

        # cd /etc/yum.repos.d

    - #### 安装RPMFusion源：

        	# rpm -ivh http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm
    		# rpm -ivh http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm

    - #### 安装FZUG源（中文Fedora社区的软件源）：

        # dnf config-manager --add-repo=http://repo.fdzh.org/FZUG/FZUG.repo

    - #### 163源(添加到当前目录下)

        	# wget http://mirrors.163.com/.help/fedora-163.repo
        	# wget http://mirrors.163.com/.help/fedora-updates-163.repo

        安装好了源之后，使用命令

            dnf makecache

        将服务器上的软件包信息在本地进行缓存，以提高搜索和安装软件的速度

    	   sudo dnf clean all && sudo dnf autoremove
    	   sudo dnf update && sudo dnf upgrade

- ### console 安装程序

        sudo dnf install

            nautilus-open-terminal gcc-c++ vim  vlc gnome-tweak-tool lantern chromium thunderbird p7zip unar gimp zeal qbittorrent
            nmap wireshark  

- ### extenstoin

        sudo dnf install gnome-shell

    [extension 安装下载地址: https://extensions.gnome.org/](https://extensions.gnome.org/)
    > 网页方式安装各扩展

启用|拓展|如下
---|---|---
coverflow alt-tab|dash to dock|drop down terminal
dynamic top bar|hide top bar|netspeed
openweather|gtile|

- ### 各种应用程序

    + #### fcitx

        * ##### 安装输入法

        	使用dnf安装fcitx，这里fcitx-configtool是fcitx的配置图形界面

            	sudo dnf install fcitx fcitx-pinyin fcitx-configtool fcitx-cloudpinyin

        * ##### 安装图形管理依赖

        	很多人说到fcitx安装成功了，配置也配置好了，在浏览器或者其他应用里面可以用，但在terminal中就不能使用，这是因为没有装fcitx的图形管理包所导致的。kde依赖于qt5,而gnome依赖于gtk3

        	kde界面使用：  

            	sudo dnf install fcitx-qt5

        	gnome界面使用：  

            	sudo dnf install fcitx-gtk3

        * ##### 安装输入法选择器

	        这里使用im-chooser

	            sudo dnf install im-chooser

        * ##### 安装完成后在终端中运行im-chooser选择fcitx，注销后继续

        * ##### 选择输入法

        	打开fcitx-configtool,添加pinyin输入法，至此就成功完成了输入法的安装。

	+ #### atom

			sudo dnf install atom

		* ##### MarkDown

				打开 preview 模式（ctrl + shift + m）
				右键保存为 html
				浏览器打开，便可以转成 pdf

    + #### Goldendict
    > 图像语音等压缩包内的文件解压到同一文件夹下

			sudo dnf install goldendict

	    * 安装 mplayer 播放读音

	        	sudo dnf install mplayer

        * 字典文件（百度网盘）

	            Longman Pronunciation Dictionary for Lingvo     #朗文5
	            MWCollegiate for Lingvo     #韦伯11
	            OALD8 for Lingvo    #牛津8

    + #### Albert

        	sudo dnf copr enable rabiny/albert
        	sudo dnf install albert    	
        [reference](http://www.2daygeek.com/install-albert-app-application-launcher-arch-linux-mint-debian-fedora-ubuntu/)

    + #### Zsh

        * ##### 安装 zsh:

        		sudo dnf install zsh

        * ##### 安装 oh my zsh:

            $ git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh

		1. If you already have an existing ~/.zshrc file, create a backup:
			cp ~/.zshrc ~/.zshrc.orig
		3. Create a new zsh config by copying the zsh template we’ve provided.
			cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
		4. Set zsh as your default shell:
			chsh -s /bin/zsh
		5. Restart ZSH

		* ##### 安装插件

				sudo dnf install autojump
		        sudo dnf install autojump-zsh

    + #### netease-cloud-music

        1. 下载deb包

            http://music.163.com/#/download
            > 官网的是.deb格式的,而我们fedora需要的是rpm格式的,看到网上很多都是把这deb转为rpm，测试了一下，总是报错，放弃了

        1. 将这个包里面的usr文件夹解压出来，其余的无用
        1. 将usr里面的文件对应着目录移到系统中/usr文件夹中下

                sudo mv ~/Downloads/usr/bin/netease-cloud-music /usr/bin
                sudo mv ~/Downloads/usr/lib/netease-cloud-music /usr/lib
                sudo mv ~/Downloads/usr/share/applications/netease-cloud-music.desktop /usr/share/applications/
                sudo mv ~/Downloads/usr/share/doc/netease-cloud-music /usr/share/doc
                sudo mv ~/Downloads/usr/share/icons/hicolor/scalable/apps/netease-cloud-music.svg    /usr/share/icons/hicolor/scalable/apps

        1. 将图标改成网易云音乐的
            > 定位到/usr/share/applications/ 中，打开那个快捷方式，就可以了，用记事本打开，将图标改成网易云音乐的

                Icon=/usr/share/icons/hicolor/scalable/apps/netease-cloud-music.svg

        1. 加音视频解码器，不然会报网络错误

                su -c 'dnf install http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm'
                sudo dnf install gstreamer1-libav gstreamer1-plugins-ugly gstreamer1-plugins-bad-free gstreamer1-plugins-bad-freeworld gstreamer1-vaapi
                sudo dnf install libmad

        1. 加两条命令
        
                sudo dnf install qt5-qtx11extras
                sudo dnf install qt5-qtmultimedia

        1. ok

    + #### sublime text 3
    > fedora 需要选择 tarball 版本。下载后将 sublime text 3 解压后放到 opt 目录下。这是默认位置，你也可以选择其他路径，对应进行修改。

        1. 假定下载到 /home/Download下载 目录下，为了方便，我们直接用归档管理器打开，将压缩包里的文件拉到 /home/hioeb 下。重命名文件夹名称为 sublime_text。同样也是默认命名。
        
        1. 接着，我们打开 shell ，切换到 root 权限，执行拷贝操作：
        
                sudo su
                cp -r /home/Download/sublime_text /opt

        1. 如果我们想在命令行下键入 sublime 就启动 sublime text ，我们可以执行以下命令，建立软链接：
               
               ln -s /opt/sublime_text/sublime_text /usr/bin/sublime
            > 确保路径正确

        1. 如果我们还想添加到收藏夹，方便打开，那么我们还需要将 sublime_text.desktop 文件拷贝到 /usr/share/applications/ 目录下

        我们就可以在 Gnome 3 的应用程序列表里看到 sublime_text 了，如果要添加到收藏夹，右键就有了。（这个步骤，要打开这个文件确保里面的路径都是正确，图片是合适的）

    + #### virtualbox

        - ##### 下载
        
            [Download：https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)

        - ##### 预处理

                sudo update
                sudo dnf install kernel kernel-devel
            > 如果创建虚拟机时出错，则按照提示进行操作

        - ##### 安装、新建虚拟机

        - ##### 安装 Vbox Addtions

            安装好系统后，安装工具包VBoxGuestAdditions.iso（）
            这个映像文件位于VirtualBox的安装目录下，/usr/share/virtualbox
            在VirtualBox控制面板中，点击“settings”，接着选“storage”，加载映像。启动虚拟机后，安装辅助工具包。

			> 若使用命令行方式安装，可能不存在 iso 文件，需要下载好软件包，然后从中解压出 iso 文件

		- ##### 设置共享目录
		> 安装好增强工具以后才可用

            1. 在 VirtualBox 先选择你的虚拟系统，接着“settings”，选“shared folders”，点击添加。设置好共享的文件夹及其名字，例如名字取为 Documents
            2. 接着启动进入客户机 Windows，打开“我的电脑”，依次点击菜单栏“工具”－“映射网络驱动器”，驱动器盘符自选，文件夹填“\\\vboxsvr\Documents”，Documents 是之前设置的共享文件夹的名称
            3. 确定后,在“网络驱动器”那里就可以看到共享文件夹的盘标了

	        ##### 遇到的问题：

	            1. 直接在共享文件夹中使用应用程序打开文件，修改后不能直接保存，如用Photoshop打开某图片并修改后，ctrl+s不能保存，提示该文件已经被锁定
				2. 安装 Vbox Addtions 后，windows 10 无法打开
				3. 安装 Vbox Addtions 后，虚拟机显示界面花屏

	        ##### 解决办法：

	            1. 把共享文件夹中的文件复制到Windows的本地磁盘中，修改完成后，再复制回共享文件夹
				2. 开机按 F8 进入安全模式，卸载 Vbox Addtions
				3. 关闭 “display” 中的 2D、3D 加速选项

- ### 问题汇总

    + #### Enabling DNF’s Fastest Mirror Plugin

    I’ve found that the fastestmirror plugin helps reduce times for downloads and updates, so enabling it is the first thing that I do.  Use the editor of your choice for the below – my example uses gedit, since it’s already installed by default.

        sudo gedit /etc/dnf/dnf.conf
        Add the below line to the bottom of the file, then you’re done.

        fastestmirror=true
        Save and exit the file.

    + #### mv

        ##### Argument list too long

    > 到所移动的文件夹下进行操作

            ls . | xargs -t -I {} mv {} target_path/{}
            ls . | xargs -t -I {} mv {} ../{}

        ##### 移动某文件夹下全部文件

            mv ./*

    + #### ls

        只显示文件夹     
			ls -l | grep ^d
        只显示文件         
			ls -l | grep ^-

		查看文件和文件夹大小

            df可以查看一级文件夹大小、使用比例、档案系统及其挂入点
            du查询文件或文件夹的磁盘使用空间        
        > 参数 -h 表示使用「Human-readable」的输出，也就是在档案系统大小使用 GB、MB 等易读的格式

        > -h 对 ls 命令也有效，但只针对文件

        如果当前目录下文件和文件夹很多，使用不带参数du的命令，可以循环列出所有文件和文件夹所使用的空间。这对查看究竟是那个地方过大是不利的，所以得指定深入目录的层数，参数：--max-depth=，这是个极为有用的参数！如下，注意使用“ * ”，可以得到文件的使用空间大小.

    + #### Adobe Flash Player 26 on Fedora 26/25

    [reference](https://www.if-not-true-then-false.com/2010/install-adobe-flash-player-10-on-fedora-centos-red-hat-rhel/)

        * ##### Adobe Repository 64-bit x86_64

                # rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm
                # rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux

        * ##### Fedora 26/25/24
                # dnf install flash-plugin alsa-plugins-pulseaudio libcurl

- ### 待办

        xmind
        fingerprint driver
