### make

用于自动编译、链接程序的实用工具。使用make后就不需要手工编译每个程序文件。

要使用make，首先要编写makefile，makefile描述程序文件之间的依赖关系以及提供更新文件的命令。

在一个程序中，可执行文件依赖于目标文件，而目标文件依赖于源文件。

如果 makefile 文件存在，每次修改完源程序后，用户通常所需要做的事情就是在命令行敲入“make”，然后所有的事情都由 make 来完成。

makefile 文件用来告诉 make 需要做的事情，通常指怎样编译、怎样链接一个程序。

command format

    make [-f makefile] [option] [target]…

make命令后跟 -f 选项，指定makefile的名字为makefile

target是make指定的目标。

eg:makefile的名字是my_hello_make：

    make –f my_hello_make
