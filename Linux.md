# 网络
1. Linux配置IP地址配置
    * ifconfig 命令查看网络配置：`ifconfig ens33 IP_addr mask `
    ```
    UP：表示生效；<br>
    BRODCAST：表示支持组播；<br>
    MULTICAST：表示支持多播；<br>
    txqueuelen：缓冲区大小；<br>
    RX：接收情形；TX：传送情形；
    ```
    * 修改网络配置文件，/etc/sysconfig/network-scripts/ifcfg-ens33
    ```
    这里注意 etc是and so on 来源于法语 et cetera，译为等等；Linux的配置文件一般放在这个文件夹下，意为零碎的东西
    ```
