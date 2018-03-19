# Configuration

<!-- MarkdownTOC -->

- 添加源
- root 用户
- 软件
- 多系统启动项修改

<!-- /MarkdownTOC -->

### 添加源

- #### 保存源配置文件的原文件

        sudo mv /etc/apt/sources.list /etc/apt/sources.list.save

- #### 新增阿里云源

        sudo vim /etc/apt/sources.list

        deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
        deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
        deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
        deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
        deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
        deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
        deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
        deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
        deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
        deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse

### root 用户

Ubuntu 的默认 root 密码是随机的，即每次开机都有一个新的 root 密码。 但我们可以

    sudo passwd su

### 软件

软件包管理工具 gdebi

    sudo apt install gdebi

### 多系统启动项修改

丢失 win10 启动项

    sudo update-grub2

others

    sudo vim /etc/default/grub
