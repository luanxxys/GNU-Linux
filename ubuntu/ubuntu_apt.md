APT（Advanced Packaging Tool，高级软件包管理工具），由 Debian 首创，它用于方便而高效地进行软件包的安装，能自动处理软件相互之间的依赖关系，并且在软件包升级过程中维护好配置文件。

1. 软件包安装

    apt install <deb_name>
    auto-apt run <command>
    > 这条命令可以自动安装包含缺失文件的软件包

1. 软件包维护

    apt update
    > 在你更改了/etc/apt/sources.list 或 /etc/apt/preferences 后，需要运行这个命令以令改动生效

    apt upgrade
    > 更新所有已安装的软件包

    apt -f install
    > 等同于 gdebi 软件包管理器中的“编辑->修正（依赖关系）损毁的软件包”再点击“应用”

    apt autoclean
    > 如果你的硬盘空间不大的话，可以定期运行这个程序，将已经删除了的软件包的.deb安装文件从硬盘中删除掉

    apt clean
    > 类似上面的命令，但它删除包缓存中的所有包

1. 软件包维护

    dpkg-reconfigure foo
    > 重新配置“foo”包

    echo "foo hold" | dpkg --set-selections
    > 设置包“foo”为hold，不更新这个包，保持当前的版本，当前的状态，当前的一切

    echo "foo install" | sudo dpkg --set-selections
    > 删除“hold”“locked package”状态设置


1. 软件包删除

    apt remove <deb_name>
    > 删除已安装的软件包（保留配置文件）

    apt --purge remove <deb_name>
    > 删除已安装包（不保留配置文件）

    apt autoremove
    > 删除为了满足其他软件包的依赖而安装的，但现在不再需要的软件包


1. 软件包搜索

    apt-cache search foo
    > 搜索和"foo"匹配的包

    apt-cache show foo
    > 显示"foo"包的相关信息，例如描述、版本、大小、依赖以及冲突

    dpkg -l *foo*
    > 查找包含有"foo"字样的包

    dpkg -L foo
    > 显示名为“foo”的包都安装了哪些文件以及它们的路径

    dlocate foo
    > 在已安装的包中搜索“foo”的文件

    apt-cache pkgnames
    > 快速列出已安装的软件包名称

