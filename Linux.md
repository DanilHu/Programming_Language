# 网络
1. Linux配置IP地址配置
    * ifconfig 命令查看网络配置：`ifconfig ens33 IP_addr mask `
    ```
    UP：表示生效；
    BRODCAST：表示支持组播；
    MULTICAST：表示支持多播；
    txqueuelen：缓冲区大小；
    RX：接收情形；TX：传送情形；
    ```
    * 修改网络配置文件
    1. /etc/sysconfig/network-scripts/ifcfg-ens33
    ```
    这里注意 etc是and so on 来源于法语 et cetera，译为等等；Linux的配置文件一般放在这个文件夹下，意为零碎的东西
    文件内容如下：
    TYPE="Ethernet"		#网卡类型（通常是Ethemet以太网）
    PROXY_METHOD="none"	#代理方式：为关闭状态
    BROWSER_ONLY="no"	#只是浏览器：否
    BOOTPROTO="static"	#网卡的引导协议【static：静态IP  dhcp：动态IP   none：不指定，不指定容易出现各种各样的网络受限】
    DEFROUTE="yes"		#默认路由
    IPV4_FAILURE_FATAL="no"		#是否开启IPV4致命错误检测
    IPV6INIT="yes"		#IPV6是否自动初始化：是（现在还未用到IPV6，不会有任何影响）
    IPV6_AUTOCONF="yes"	#IPV6是否自动配置：是（现在还未用到IPV6，不会有任何影响）
    IPV6_DEFROUTE="yes"	#IPV6是否可以为默认路由：是（现在还未用到IPV6，不会有任何影响）
    IPV6_FAILURE_FATAL="no"		#是否开启IPV6致命错误检测
    IPV6_ADDR_GEN_MODE="stable-privacy"	#IPV6地址生成模型
    NAME="ens33"		#网卡物理设备名称
    UUID="ab60d501-535b-49f5-a76b-3336a4120f64"#通用唯一识别码，每一个网卡都会有，不能重复，否则两台linux机器只有一台可上网
    DEVICE="ens33"		#网卡设备名称，必须和‘NAME’值一样
    ONBOOT="yes"		#是否开机启动，要想网卡开机就启动或通过 `systemctl restart network`控制网卡,必须设置为 `yes`
    IPADDR=192.168.137.129		# 本机IP
    NETMASK=255.255.255.0		#子网掩码
    GATEWAY=192.168.137.2		#默认网关
    DNS1=8.8.8.8#
    DNS2=8.8.8.5#
    ZONE=public#
    通过修改其中的IPADDR和NETMASK和GATEWAY就可以更改IP地址了
    ```
    2. /etc/sysconfig/network<br>
    ```
    命令：hostname也可以查看和临时修改主机名
    文件内容如下：
    NETWORKING=yes # 代表正在运行
    HOSTNAME=localhost.localdomain # 标识主机名，Linux的主机名可以是一样的
    ```
    3. /etc/resolv.conf
    ```
    nameserver IPaddr
    标识DNS服务器<br>
    ```
    > DNS：域名服务器，每一个域名服务器管理一个区，这个服务器上存储的是该区内所有的主机名到其IP地址的映射<br>
    DHCP：DHCP（动态主机配置协议）是一个局域网的网络协议。指的是由服务器控制一段IP地址范围，客户机登录服务器时就可以自动获得服务器分配的IP地址和子网掩码，因此需要在局域网内有DHCP服务器才行(局域网本身的设计就是用来短距离通信的，只要网线连在一起就不需要访问互联网可以直接通信)。<br>
    路由协议：指导路由器中路由表的生成；包括内部网关协议`RIP——路由信息协议(Routing Information Protocol)`，内部网关协议`OSPF——开放最短路径优先(Open Shortest Path First)`，外部网关协议`BGP——边界网关协议`
# 基本操作
1. 命令行快捷键
   ```
   常用：
   Ctrl L ：清屏
   Ctrl M ：等效于回车
   Ctrl C : 中断正在当前正在执行的程序
   历史命令：
   Ctrl P : 上一条命令，可以一直按表示一直往前翻
   Ctrl N : 下一条命令
   Ctrl R，再按历史命令中出现过的字符串：按字符串寻找历史命令（重度推荐）
   命令行编辑：
   Tab : 自动补齐（重度推荐）
   Ctrl A ： 移动光标到命令行首
   Ctrl E : 移动光标到命令行尾
   Ctrl B : 光标后退
   Ctrl F : 光标前进
   Alt F : 光标前进一个单词
   Alt B : 光标后退一格单词
   Ctrl ] : 从当前光标往后搜索字符串，用于快速移动到该字符串
   Ctrl Alt ] : 从当前光标往前搜索字符串，用于快速移动到该字符串
   Ctrl H : 删除光标的前一个字符
   Ctrl D : 删除当前光标所在字符
   **Ctrl K ：删除光标之后所有字符**
   Ctrl U : 清空当前键入的命令
   Ctrl W : 删除光标前的单词(Word, 不包含空格的字符串)
   Ctrl \ : 删除光标前的所有空白字符
   Ctrl Y : 粘贴Ctrl W或Ctrl K删除的内容
   Alt . : 粘贴上一条命令的最后一个参数（很有用）
   Alt [0-9] Alt . 粘贴上一条命令的第[0-9]个参数
   Alt [0-9] Alt . Alt. 粘贴上上一条命令的第[0-9]个参数
   Ctrl X Ctrl E : 调出系统默认编辑器编辑当前输入的命令，退出编辑器时，命令执行
   其他：
   Ctrl Z : 把当前进程放到后台（之后可用''fg''命令回到前台）
   Shift Insert : 粘贴（相当于Windows的Ctrl V）
   在命令行窗口选中即复制
   在命令行窗口中键即粘贴，可用Shift Insert代替
   Ctrl PageUp : 屏幕输出向上翻页
   Ctrl PageDown : 屏幕输出向下翻页
   ```
2. find命令，find的目录在中间，参数在后面
   > 常用指令：<br>
   `find ./ maxdepth 1 -type 'l'`按照类型找，后面指定的是路径和查找深度，默认查找深度是最大深度。Linux下的文件就系统定义的七种类型。目录，普通文件。软连接，硬链接……<br>
   `find ./ maxdepth 1 -name '*.mp3'`按照名字找<br>
   `find ./ -size +20M -size -50M`按照大小查找，可以大于20M小于50M。注意的是size必须不能掉，且必须是大写的M。kb的话就必须是小写，可以使用man来查看 <br>
   `find ./ -atime/-mtime/-ctime `按照时间，这里有三个时间，分别是最近访问(attend)，最近更改(属性，比如硬链接和软连接数。modify)，最近更改(内容,change)，这个是按天，cminit按分钟。<br>
   `find ./ -type f -exec ls -l {} \;`后面的;是语句的结束，shell编程需要这个;，因此需要转义。-exec可以转换为ok，来询问
3. grep命令
   > 常用指令：<br>
   `grep -r 'copy' ./ -n`找当前目录下(-r代表递归)下文件中含有copy字符的文件，并给出行号<br>
   `ps aux`显示当前所有的进程，a代表all，u代表usr，x代表显示不需要交互的进程<br>
   `ps aux | grep kernel`利用管道来查找当前所有进程中包含所需东西 的内容
# makefile
就是为了省掉没改变的文件的编译时间<br>
1个规则：
   1. 若想生成目标，检查规则中的依赖条件是否存在，如果不存在，则寻找是否有规则用来生成该依赖文件。
   2. 当依赖的最后修改时间比目标晚的时候make就知道这个文件被改动过，则需要重新根据命令执行一遍。
   3. makefile默认的是第一个目标的规则当作最终目标，只要生成了就不管了但是可以通过`All`命令来指定最终文件：`ALL:a.out`
```C
目标：依赖
   (一个tab缩进)命令
hello:hello.o  // hello.o没有，所以先检查是否有其他规则生成hello.o
   gcc hello.o -o hello
hello.o:hello.c
   gcc -c hello.c -o hello.o
```
2个函数
   1. wildcard
   ```
   src = $(wildcard ./*.c)  // 将.c文件结尾的文件名匹配并且将结果返回给src，以列表的方式
   ```
   2. patsubst
   ```
   obj = $(patsubst %.c, %.o, $(src))  // 将参数3中，包含参数1的部分，替换为参数2
   ```
   3. clean，算是一个规则，没有依赖的规则
   ```
   clean:
      -rm -rf $(obj) a.out // -，表示出错依然执行
   可以单独执行 make clean -n，模拟执行，然后删掉-n再真正执行 
   ```
3个自动变量<br>
自动变量只能出现在规则的命令部分
   1. $@：表示规则中的目标
   2. $<：表示第一个依赖条件，如果应用到模式规则，可将依赖条件列表中的依赖一次取出，套用模式规则
   3. $^：表示所有依赖规则
模式规则<br>
方便修改源代码，增加文件或删减文件
   ```
   %.o:%.c
      gcc -c $< -o $@
   ```
静态模式规则<br>
为了避免make找不到正确的模式
   ```C
   $(obj):%.o:%.c // 要生成obj找这个规则
      gcc -c $< -o $@
   ```
防止clean文件，对makefile中的clean造成影响，因为clean再makefile中就类似一个目标。因此需要把makefile里面的clean生成伪目标，.PHONY，就是不管条件满足与否都会执行clean 和 ALL。可以再makefile里面加参数
```
myargs = -g -Wall //这样生成的可以直接调试且带警告信息
.PHONY: clean all
```
# 系统编程
## PCB 进程控制块
1. 是一个结构体，再sched.h头文件中，task_struct结构体
2. 描述当前进程，也称为进程描述符
3. 包含以下内容(重要内容)
   > 进程id，实际上在C语言中用pid_t表示<br>
   进程的状态，初始、就绪、运行、挂起、停止<br>
      **挂机的进程会主动放弃CPU**<br>
   进程切换的时候需要保存和恢复的一些CPU寄存器<br>
   描述虚拟地址空间的信息<br>
   描述控制终端的信息<br>
   当前工作目录<br>
   umask掩码<br>
      **指定新创建的文件的类型**<br>
   文件描述符表，包含很多指向file结构体的指针<br>
   用户id和组id<br>
   会话和进程组<br>
   进程可以使用的资源上限
## 父子进程共享的资源
1. 全局变量、.data、.text、栈、堆、环境变量、用户ID、宿主目录、进程工作目录、信号处理方式相同。不同的地方在于：进程ID、fork返回值、父进程ID、进程运行时间<br>
`几乎0~3G用户空间内容和父进程的PCB都相同，但是并不是每一个子进程都拷贝一份然后映射到物理内存，而是遵循读时共享、写时复制的原则，就是只读的时候不复制，但是要改的时候就会重新复制一份再改`
## gdb父子进程调试
```C
set follow-fork-mode child //跟踪子进程逻辑
set follow-fork-mode parent // 跟踪父进程逻辑
```
须在fork之前打断点
## 进程间通信
父子进程之间在内核空间是共享的，因为内核只有一份。内核间有一个4096字节大小的缓冲区。
### 管道通信(使用最简单的方法，但是只能在有血缘关系的进程间通信)
> 本质是一个伪文件，就是不占用磁盘空间的文件，只占据当前进程的内存空间<br>
有两个文件描述符引用，一个是写端，一个是读端<br>
局限性：<br>
- 不能自己写，自己读
- 不可反复读取，一旦读奏，管道中的数据将不复存在
- 数据只能单方向流动
1. 利用pipe()函数可以创建这个缓冲区，创建并打开管道；即在父进程执行这个函数的时候，相当于就是父进程拿到两个文件描述符——管道的读端和写端
```C
int pipe(int fd[2])
fd[0]读端
fd[1]写端
成功返回0，失败返-1，设置errno
```
2. fork之后，子进程和父进程共享文件描述符，因此他也拿到了两个文件描述符，能够操作这个管道
3. 如果想让父进程写，子进程读，那么父进程应该关闭读端，子进程关闭写端
```C
close(fd[1])
close(fd[0])
```
4. 管道读写行为
   > 读管道<br>
   管道中有数据，read返回实际读到的字节数<br>
   管道中无数据：
   - 管道写端全部被关闭，read返回0(好像读到文件结尾)
   - 写端没有全部被关闭，read阻塞等待(此时会让出CPU资源)
   写管道<br>
   - 读端被全部关闭（说明没人想读），进程异常终止
   - 读端没有全部关闭。若管道已满，则write阻塞，否则write将数据写入，并返回实际写入字节数
5. 常见的文件描述符
   > 标准输入 stdin 文件描述符0<br>
   标准输出 stdout 文件描述符1<br>
   标准错误 stderr 文件描述符2<br>
   dup2(oldfd, newfd) 把oldfd的内容拷贝到newfd中，这样可以实现重定向。比如dup2(fd, STDOUT_FILENO)，那么文件描述符1相当于现在指向的不是标准输出，而实fd指向的文件<br>
      
