### add sources

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

Ubuntu的默认root密码是随机的，即每次开机都有一个新的root密码。 但我们可以：

    sudo passwd

        Password: <--- 输入安装时那个用户的密码
        Enter new UNIX password: <--- 新的Root用户密码
        Retype new UNIX password: <--- 重复新的Root用户密码
        passwd：已成功更新密码

### 软件

软件包管理工具 gdebi

    sudo apt install gdebi

### 多系统启动项修改

    sudo vim /etc/default/grub
