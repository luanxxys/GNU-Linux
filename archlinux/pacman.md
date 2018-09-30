# Pacman

1. ### 同步源并更新系统

        # pacman -Syu

    如果你已经使用 pacman -Sy 将本地的包数据库与远程的仓库进行了同步，也可以只执行

        # pacman -Su

1. ### 安装包

        # pacman -S <package_name>
    > 你也可以同时安装多个包，只需以空格分隔即可

    在同步包数据库后再执行安装

        # pacman -Sy <package_name>

    在显示一些操作信息后执行安装

        # pacman -Sv <package_name>

    安装本地包，其扩展名为 pkg.tar.gz

        # pacman -U <package_name>

    升级时不升级包

        # pacman pacman -Su --ignore <package_name>

1. ### 删除包

    只删除包，不包含该包的依赖

        # pacman -R <package_name>

    在删除包的同时，也将删除其依赖

        # pacman -Rs <package_name>

    删除包和它依赖的包

        # pacman -Rsc abc

    在删除包时不检查依赖

        # pacman -Rd <package_name>

1. ### 搜索包

    搜索含关键字的包

        # pacman -Ss <package_name>

    查看有已经安装的包的信息

        # pacman -Qi <package_name>

    > 用 -Q 标志搜索和查询本地包数据库

    列出该包的文件

        # pacman -Ql <package_name>

1. ### 其他用法

    只下载包，不安装

        # pacman -Sw <package_name>

    清理未安装的包文件

        # pacman -Sc Pacman
    > 下载的包文件位于 /var/cache/pacman/pkg/ 目录

    清理所有的缓存文件

        # pacman -Scc

    清理孤立的程序

        # pacman -Qdt

[Archlinux:Pacman (简体中文)](https://wiki.archlinux.org/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))
