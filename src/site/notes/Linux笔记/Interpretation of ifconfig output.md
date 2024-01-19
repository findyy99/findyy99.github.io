---
{"dg-publish":true,"permalink":"/Linux笔记/Interpretation of ifconfig output/","tags":["Linux"]}
---

```bash
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:ae:71:c7:0a  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

enp0s5: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.211.55.12  netmask 255.255.255.0  broadcast 10.211.55.255
        inet6 fdb2:2c26:f4e4:0:21c:42ff:feca:2cdd  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::21c:42ff:feca:2cdd  prefixlen 64  scopeid 0x20<link>
        ether 00:1c:42:ca:2c:dd  txqueuelen 1000  (Ethernet)
        RX packets 423  bytes 276453 (269.9 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 332  bytes 33369 (32.5 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```


这是通过运行`sudo ifconfig`命令获取的网络接口信息。以下是对输出中每个网络接口的解释：

1. **docker0:**
   - **flags:** 网络接口的标志，此处包括UP（已启动）、BROADCAST（支持广播）和MULTICAST（支持多播）等。
   - **mtu:** 最大传输单元，指定在单个网络层上通过一个连接传送的最大数据包大小。
   - **inet:** 接口的IPv4地址（172.17.0.1）。
   - **netmask:** 掩码，用于确定网络上的主机和网络部分。
   - **broadcast:** 广播地址，用于向网络上所有主机发送数据。
   - **ether:** 以太网地址（MAC地址）。
   - **txqueuelen:** 发送队列的长度。
   - **RX packets/bytes:** 接收的数据包和字节数。
   - **TX packets/bytes:** 发送的数据包和字节数。
   - **RX errors/TX errors:** 接收和发送的错误数量。
   - **dropped:** 丢弃的数据包数量。
   - **overruns:** 接收或发送缓冲区溢出次数。
   - **frame:** 接收到的帧错误次数。
   - **carrier:** 与载波相关的错误数量。
   - **collisions:** 发送时的碰撞次数。

2. **enp0s5:**
   - 类似于docker0，但这是物理网络接口。
   - **inet:** 接口的IPv4地址（10.211.55.12）。
   - **netmask:** 掩码，用于确定网络上的主机和网络部分。
   - **broadcast:** 广播地址，用于向网络上所有主机发送数据。
   - **ether:** 以太网地址（MAC地址）。
   - **inet6:** IPv6地址和相关信息。
   - **txqueuelen:** 发送队列的长度。
   - **RX packets/bytes:** 接收的数据包和字节数。
   - **TX packets/bytes:** 发送的数据包和字节数。
   - **RX errors/TX errors:** 接收和发送的错误数量。
   - **dropped:** 丢弃的数据包数量。
   - **overruns:** 接收或发送缓冲区溢出次数。
   - **frame:** 接收到的帧错误次数。
   - **carrier:** 与载波相关的错误数量。
   - **collisions:** 发送时的碰撞次数。

3. **lo ([Loopback](https://www.baeldung.com/linux/loopback-lo-device)):**
   - **flags:** 网络接口的标志，包括UP（已启动）和LOOPBACK（环回）。
   - **mtu:** 最大传输单元，65536表示Loopback接口支持非常大的数据包。
   - **inet:** 环回接口的IPv4地址（127.0.0.1）。
   - **netmask:** 掩码，用于确定网络上的主机和网络部分。
   - **inet6:** IPv6地址和相关信息。
   - **loop:** 发送队列的长度。
   - **RX packets/bytes:** 接收的数据包和字节数。
   - **TX packets/bytes:** 发送的数据包和字节数。
   - **RX errors/TX errors:** 接收和发送的错误数量。
   - **dropped:** 丢弃的数据包数量。
   - **overruns:** 接收或发送缓冲区溢出次数。
   - **frame:** 接收到的帧错误次数。
   - **carrier:** 与载波相关的错误数量。
   - **collisions:** 发送时的碰撞次数。