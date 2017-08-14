### linux下删除目录及其子目录下某种类型文件

Linux下，如果想要删除目录及其子目录下某种类型文件，比如说所有的txt文件，则可以使用下面的命令：
[html] view plain copy print?
find . -name " *.txt " -type f -print -exec rm -rf {} \;  

. : 表示在当前目录下
[html] view plain copy print?
-name "*.txt"  

表示查找所有后缀为txt的文件
[html] view plain copy print?
-type f  

表示文件类型为一般正规文件
[html] view plain copy print?
-print  

表示将查询结果打印到屏幕上
[html] view plain copy print?
-exec command  

command为其他命令，-exec后可再接其他的命令来处理查找到的结果，上式中，{}表示”由find命令查找到的结果“，如上所示，find所查找到的结果放置到{}位置，-exec一直到”\;“是关键字，表示find额外命令的开始（-exec）到结束（\;），这中间的就是find命令的额外命令，上式中就是 rm -rf
