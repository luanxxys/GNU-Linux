### bin
> bin 就是二进制（binary）英文缩写，可执行二进制文件的目录，如常用的命令ls、tar、mv、cat等

### sbin
> 放置系统管理员使用的可执行命令，如fdisk、shutdown、mount等。与bin不同的是，这几个目录是给系统管理员root使用的命令，一般用户只能“查看”而不能设置和使用。像典型的poweroff命令。

### root
> root用户的主目录。

### lib
> lib是库（library）英文缩写。该目录是根文件系统上的程序所需的共享库，存放了根文件系统程序运行所需的共享文件。

lib/modules：包含系统核心可加载各种模块，尤其是那些在恢复损坏的系统时重新引导系统所需的模块(例如网络和文件系统驱动)

### home
> 系统默认的用户主目录，新增用户账号时，用户的主目录都存放在此目录下，~表示当前用户的主目录。如果建立一个用户，用户名是“test”，那么在home目录下就有一个对应的home/test路径，用来存放用户的主目录。
>
>可以单独分区，并设置较大的磁盘空间，方便用户存放数据

### lost+fount
> 系统异常产生错误时，会将一些遗失的片段放置于此目录下，通常这个目录会自动出现在装载目录下

### mnt/media 
> mount,光盘默认挂载点。这个目录在一般情况下也是空的。可以临时将别的文件系统挂在这个目录下，通常光盘
挂载于mntcdrom下。

### opt
> option,给主机额外安装软件所摆放的目录。如：FC4使用的Fedora 
社群开发软件，如果想要自行安装新的KDE 桌面软件，可以将该软件安装在该目录下。以前的 Linux 系统中，习惯放置在 usrlocal 目录下。

### tmp 
> temporary,用来存放不同程序执行时产生的临时文件

### srv
> service,服务启动之后需要访问的数据目录，如www服务需要访问的网页数据存放在srvwww内
etc、bin、dev、lib、sbin应该和根目录放置在一个分区中

### boot
> 在这个目录下存放的都是系统启动时要用到的程序
> 
> boot可以单独分区，如果单独分区，建议分区大小为100M

directory|description
---|---
boot/vmlinuz|linux的内核文件
boot/gurb|存放的是引导程序

### dev
> dev 是设备（device）的英文缩写。这个目录中包含了所有linux系统中使用的外部设备，但是这里并不是放的外部设备的驱动程序。访问该目录下某个文件，相当于访问某个设备，常用的是挂载光驱mount devcdrom mnt。

### etc
> etcetera,这个目录下存放了系统管理时要用到的各种配置文件和子目录。

directory|description
---|---
etc/fstab|这个文件会列出当前系统在启动时自动安装的所有文件系统，也包括用swapon-a启用的swap区的信息。可以使用mount –a这个命令来手动地安装这个文件中列出的所有文件系统。另外，可以通过修改这个设置文件，使系统在启动时自动安装我们所需要的其他文件系统。
etc/group|列出有效的组名称及组中的用户信息
etc/passwd|帐号的密码文件:帐号 密码 用户号UDI 用户组号GID 所属组 用户主目录 用户所使用的shell
etc/shadow|包括加密后的帐号信息。影子口令文件将etc/passwd文件中的加密口令移动到etc/shadow中，而后者只对超级用户可读。
etc/shells|包括系统的能使用的shell列表
etc/host.conf|告诉域名服务器怎么查找主机名
etc/hosts|网络中已发现的主机的名称列表，用于解析主机名
etc/networks|列举从机器所连接的网络能访问的网络名和网络地址，通过路由命令使用，允许使用网络名称。
etc/protocols|列举当前可用的协议
etc/resolv.conf|在程式请求“解析”一个IP地址时，告诉内核应该查询哪个名称服务器
etc/services|将网络服务器名转换为端口号协议，由inetd、telnet、tcpdump和一些其他程式读取，有一些C访问例程。

### proc
> process,虚拟的目录，是系统内存的映射。

### procx
> 关于进程x的信息目录，这一x是这一进程的标识号。每个进程在proc下有一个名为自己进程号的目录。

directory|description
---|---
proc/self|是一个连接，指向了当前运行中的进程目录。
proc/cpuinfo|是当前系统 cpu 的详细信息，从型号到支持的特性，如果你是多核 cpu 的话，会看到多个这样的输出。检测 cpu 的程序，也是通过 proc/cpuinfo 来得到当前 cpu 的详细信息的
proc/meminfo|是当前系统内存的详细信息。像 top、free 这些可以查看当前系统内存信息的程序，就是通过读取 proc/meminfo 来实现的
proc/version|是当前系统的版本信息，包括编译时间。uname 这个命令，就是通过它来得到内核版本和系统版本
proc/filesystems|为当前系统支持的文件系统列表，你可以在程序中读取这个文件，以获得当前系统对文件系统的支持信息
proc/apm APM|高级电源管理信息。
proc/acpi|目录下为 ACPI 的详细信息。 比方说, 你想知道你的笔记本电脑是否连接了电源, 你可以 cat proc/acpiac_adapterACstate 看看结果是 on line 还是 off line 。
proc/cmdline|显示内核的启动参数，一般就是你 grub 中传入内核的那些参数
proc/loadavg|显示系统的负载，w、top 这类程序也是从此得到系统负载信息。
proc/uptime|系统自启动来所经历的秒数，uptime 程序就是从此计算出系统启动后经历的时间的。
proc/devices|系统中所有可用的字符和块设备列表。Character devices|字符设备；Block devices：块设备；netlink：网络设备；lp打印机、tty终端、input输入设备
proc/iomem|IO内存映射。
proc/ioports|当前使用的IO 端口信息。
proc/dma|当前可用的 DMA 通道。
proc/mounts|系统当前的挂载信息。
proc/interrupts|显示被占用的中断信息和占用者的信息，以及被占用的数量。
proc/irq|为IRQ 信息
proc/kcore|系统物理内存映像。与物理内存大小完全一样，然而实际上没有占用这么多内存；它仅仅是在程序访问它时才被创建。(注意：除非你把它拷贝到什么地方，否则proc/下没有任何东西占用任何磁盘空间。)
proc/kmsg|Linux内核启动输出的消息。也会被送到syslog。
proc/ksyms|核心符号表。
proc/modules|存放当前加载了哪些核心模块信息。
proc/partitions|分区信息
proc/net|网络协议状态信息。
proc/stat|系统的不同状态，例如，系统启动后页面发生错误的次数。
proc/sys|目录下不仅提供了系统某些设置信息，你还可以修改这些文件来在运行中改变系统的参数，比如，你想让别人 ping 不到你，只要在终端输入以下命令的第一条，如果要恢复让别人可以拼到时你，则须终端输入第二条命令即可（但必须是管理员权限才能执行这二条命令）。proc/sys 下的可配置的选项很多，主要有 6 类： debug、dev、fs、kernel、net、vm，只要文件属性是可读写的，一般都对应了系统某个可以修改的参数。不过系统重启之后参数就恢复默认值了

### usr
> Unix System Resources，或 Unix Software Resources,或 Unix Shared Resources
> 应用程序存放的目录

directory|description
---|---
usr/bin|存放应用程序
usr/sbin|超级用户的一些管理程序
usr/share|存放共享数据
usr/sharedoc|系统说明文件存放目录
usr/shareman|程序帮助文档存放目录
usr/shareinfo|gnu信息文档
usr/lib|存放不能直接运行的，却是许多程序运行所必需的一些函数库文件
usr/include|linux下开发和编译应用程序所需要的头文件
usr/local|存放软件升级包
usr/localbin|本地增加的命令
usr/locallib|本地增加的库
usr/src|源代码，linux内核的源代码就放在usr/srclinux里

### var
> variable,放置系统执行过程中经常变化的文件

directory|description
---|---
var/catman|包括了格式化过的帮助(man)页。
var/lib|存放系统正常运行时要改变的文件。
var/local|存放usr/local中安装的程序的可变数据(即系统管理员安装的程序)。
var/lock|锁定文件。
var/log|各种程序的日志(log)文件，var/log里的文件经常不确定地增长，应该定期清除。
var/run|保存在下一次系统引导前有效的关于系统的信息文件。例如，var/runutmp包含当前登录的用户的信息。程序或服务启动后，其PID也存放在该目录下
var/spool|放置“假脱机(spool)”程序的目录，如mail、news、打印队列和其他队列工作的目录。每个不同的spool在var/spool下有自己的子目录，例如，用户的邮箱就存放在var/spoolmail中。

### sys
> system
