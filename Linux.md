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
2. 命令行快捷键
   ```
   **常用：**
   Ctrl L ：清屏
   Ctrl M ：等效于回车
   Ctrl C : 中断正在当前正在执行的程序
   **历史命令：**
   Ctrl P : 上一条命令，可以一直按表示一直往前翻
   Ctrl N : 下一条命令
   Ctrl R，再按历史命令中出现过的字符串：按字符串寻找历史命令（重度推荐）
   **命令行编辑：**
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
   **其他：**
   Ctrl Z : 把当前进程放到后台（之后可用''fg''命令回到前台）
   Shift Insert : 粘贴（相当于Windows的Ctrl V）
   在命令行窗口选中即复制
   在命令行窗口中键即粘贴，可用Shift Insert代替
   Ctrl PageUp : 屏幕输出向上翻页
   Ctrl PageDown : 屏幕输出向下翻页
   ```
