### linux上进程有5种状态：

运行：正在运行或在运行队列中等待

中断：休眠中， 受阻，在等待某个条件的形成或接受到信号

不可中断：收到信号不唤醒和不可运行，进程必须等待直到有中断发生

僵死：进程已终止, 但进程描述符存在，直到父进程调用wait4()系统调用后释放

停止：进程收到SIGSTOP、SIGSTP、SIGTIN、SIGTOU信号后停止运行

### ps 工具标识进程的5种状态码：

D 不可中断 uninterruptible sleep (usually IO)

R 运行 runnable (on run queue)

S 中断 sleeping

T 停止 traced or stopped

Z 僵死 a defunct (”zombie”) process

### ps命令参数（常用）

-A 列出所有的行程

-w 显示加宽可以显示较多的资讯

-au 显示较详细的资讯

-aux 显示所有包含其他使用者的行程

### ps -au(x) 输出格式：

USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND

USER：进程拥有者

PID：pid

%CPU：占用的 CPU 使用率

%MEM：占用的内存使用率

VSZ：占用的虚拟内存大小

RSS：占用的内存大小

TTY：终端的次要装置号码 (minor device number of tty)

### ps -au(x) 输出格式：

STAT：该进程的状态

D：不可中断的静止

R：正在执行中

S：静止状态

T：暂停执行

Z：不存在但暂时无法消除

W：没有足够的内存分页可分配

<：高优先级的进程

N：低优先级的进程

L：有内存分页分配并锁在内存

### ps -au(x) 输出格式：

START：进程开始时间

TIME：执行的时间

COMMAND：所执行的指令
