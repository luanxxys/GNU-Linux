### ls

1. 只显示文件夹

        ls -l | grep ^d

1. 只显示文件

        ls -l | grep ^-

1. 查看文件和文件夹大小

    df可以查看一级文件夹大小、使用比例、档案系统及其挂入点

    du查询文件或文件夹的磁盘使用空间        
    > 参数 -h 表示使用「Human-readable」的输出，也就是在档案系统大小使用 GB、MB 等易读的格式
    >
    > -h 对 ls 命令也有效，但只针对文件

    如果当前目录下文件和文件夹很多，使用不带参数du的命令，可以循环列出所有文件和文件夹所使用的空间。这对查看究竟是那个地方过大是不利的，所以得指定深入目录的层数，参数：--max-depth=，这是个极为有用的参数！如下，注意使用“ * ”，可以得到文件的使用空间大小
