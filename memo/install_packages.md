##### rpm

- 安装

        rpm -ivh <rpm_name>.rpm

            -i 安装软件
            -t 测试安装，不是真的安装
            -p 显示安装进度
            -f 忽略任何错误
            -U 升级安装
            -v 检测套件是否正确安装

- 卸载

        rpm –e <software_name>

> dnf 也可以

##### deb

- 安装

        dpkg -i <deb_name>.deb

- 卸载

        dpkg -e <deb_name>.deb

查询当前系统安装的软件包

    dpkg –l ‘* software_name *’

##### apt 方式安装 deb

apt install <package_name>
> 安装一个新软件包（参见下文的aptitude）

apt remove <package_name>
> 卸载一个已安装的软件包（保留配置文件）

apt --purge remove <package_name>
> 卸载一个已安装的软件包（删除配置文件）

dpkg --force-all --purge <package_name> 
> 有些软件很难卸载，而且还阻止了别的软件的应用，就可以用这个，不过有点冒险。

apt autoremove
> 因为apt会把已装或已卸的软件都备份在硬盘上，所以如果需要空间的话，可以让这个命令来删除你已经删
掉的软件

apt autoclean
> 定期运行这个命令来清除那些已经卸载的软件包的.deb文件。通过这种方式，可以释放大量的磁盘空间。
如果需求十分迫切

apt clean
> 这个命令会把安装的软件的备份也删除，不过这样不会影响软件的使用的。

apt upgrade
> 更新所有已安装的软件包

apt dist-upgrade
> 将系统升级到新版本

apt-cache search string
> 在软件包列表中搜索字符串

apt-cache showpkg pkgs
> 显示软件包信息。

apt-cache stats
> 查看库里有多少软件

apt-cache dumpavail
> 打印可用软件包列表

apt-cache show pkgs
> 显示软件包记录，类似于dpkg –print-avail。

apt-cache pkgnames
> 打印软件包列表中所有软件包的名称

##### tar.gz 源代码包安装方式

解压缩

    tar -xzvf soft.tar.gz

切换安装目录

    cd soft

为编译做好准备

    ./configure

进行软件编译

    make

完成安装

    make install

删除安装时产生的临时文件

    make clean

##### tar.bz2 源代码包安装方式

    tar -xjvf soft.tar.bz2
    cd soft
    ./configure
    make
    make install

##### 压缩包内无需安装的软件

压缩包解压后，不能编译安装，则无需安装。将压缩包内对应文件转移到相应目录下即可。

    将解压文件移动到 /usr/lib
        - $PATH这个环境变量自动涵盖了/usr/lib这个目录，不用专门去修改环境变量
    建立软链接 ln -s /path/to/software /usr/bin/sublime
    并将 *.desktop 文件放在 /usr/share/appliations/ 路径下

##### bin 文件安装

如果你下载到的软件名是 soft.bin，一般情况下是个可执行文件，安装方法如下：

    chmod +x soft.bin

    ./soft.bin
