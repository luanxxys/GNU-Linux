### find

##### 按照文件后缀查找

在 /home 目录下查找以 .txt 结尾的文件名

    find /home -name "*.txt"

同上，但忽略大小写

    find /home -iname "*.txt"

当前目录及子目录下查找所有以 .txt 和 .pdf 结尾的文件

    find . \( -name "*.txt" -o -name "*.pdf" \)

或

    find . -name "*.txt" -o -name "*.pdf"

##### 按照文件后缀排除

找出 /home 下不是以 .txt 结尾的文件

    find /home ! -name "*.txt"

##### 根据文件类型进行搜索

find . -type 类型参数

参数|类型
---|---
f|普通文件
d|目录 
l|符号连接
c|字符设备
b|块设备
s|套接字
p|Fifo

##### 基于目录深度搜索

向下最大深度限制为3 

    find . -maxdepth 3 -type f

搜索出深度距离当前目录至少2个子目录的所有文件 

    find . -mindepth 2 -type f

##### 根据文件大小进行匹配

find . -type f -size 文件大小单元

单元|
---|---
k|
M|
G|
b|块（512字节）
c|字节
w|字（2字节） 


搜索大于10KB的文件

    find . -type f -size +10k

搜索小于10KB的文件 

    find . -type f -size -10k

搜索等于10KB的文件

    find . -type f -size 10k

##### 删除匹配文件

删除当前目录下所有 .txt 文件 

    find . -type f -name "*.txt" -delete

##### 借助 -exec 选项与其他命令结合使用

找出当前目录下所有root的文件，并把所有权更改为用户tom

    find .-type f -user root -exec chown tom {} \;

上例中，{} 用于与 -exec 选项结合使用来匹配所有文件，然后会被替换为相应的文件名。 

找出自己家目录下所有的.txt文件并删除

    find $HOME/. -name "*.txt" -ok rm {} \;

-ok 和 -exec 行为一样，不过它会给出提示，是否执行相应的操作。

查找当前目录下所有.txt文件并把他们拼接起来写入到 all.txt 文件中 

    find . -type f -name "*.txt" -exec cat {} \;> all.txt

找出当前目录下所有.txt文件并以“File:文件名”的形式打印出来

    find . -type f -name "*.txt" -exec printf "File: %s\n" {} \; 

因为单行命令中 -exec 参数中无法使用多个命令，以下方法可以实现在-exec之后接受多条命令

    -exec ./text.sh {} \;

##### 搜索但跳出指定的目录

查找当前目录或者子目录下所有.txt文件，但是跳过子目录sk

    find . -path "./sk" -prune -o -name "*.txt" -print

##### 其它

要列出所有长度为零的文件 

    find . -empty 

