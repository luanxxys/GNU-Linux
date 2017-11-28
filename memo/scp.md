# SCP
> Linux SSH 远程文件/目录传输命令

scp 是 secure copy 的简写，用于在 Linux 下进行远程拷贝文件的命令，和它类似的命令有 cp，不过 cp 只是在本机进行拷贝不能跨服务器，而且 scp 传输是加密的。可能会稍微影响一下速度。

- 获取远程服务器上的文件

        scp -P 3333 root@www.vpser.net:/root/<file_name> /home/<file_name>

        -P: port 端口参数
        3333 表示更改 SSH 端口后的端口，如果没有更改 SSH 端口可以不用添加该参数
        root@www.vpser.net 表示使用 root 用户登录远程服务器 www.vpser.net
        :/root/<file_name> 表示远程服务器上的文件
        /home/<file_name> 表示保存在本地上的路径和文件名

- 获取远程服务器上的目录

        scp -P 3333 -r root@www.vpser.net:/root/lnmp0.4/ /home/lnmp0.4/

        -r 参数表示递归复制（即复制该目录下面的文件和目录）

- 将本地文件上传到服务器上

        scp -P 3333 /home/<file_name> root@www.vpser.net:/root/<file_name>

- 将本地目录上传到服务器上

        scp -P 3333 -r /home/lnmp0.4/ root@www.vpser.net:/root/lnmp0.4/

- 可能有用的几个参数

        -v 和大多数 linux 命令中的 -v 意思一样，用来显示进度。可以用来查看连接，认证，或是配置错误

        -C 使能压缩选项

        -4 强行使用 IPV4 地址

        -6 强行使用 IPV6 地址
