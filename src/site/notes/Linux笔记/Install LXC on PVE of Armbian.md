---
{"dg-publish":true,"permalink":"/Linux笔记/Install LXC on PVE of Armbian/","noteIcon":"","created":"2024-05-13T22:39:44.460+08:00","updated":"2024-05-19T21:51:09.842+08:00"}
---

https://images.linuxcontainers.org/images/

```bash
config interface 'loopback'
        option ifname 'lo'
        option proto 'static'
        option ipaddr '127.0.0.1'
        option netmask '255.0.0.0'

config interface 'wan'
        option ifname 'eth0'
        option proto 'dhcp'

config interface 'wan6'
        option ifname 'eth0'
        option proto 'dhcpv6'
```


```bash
pct create 100 /mnt/KingSton/template/cache/immortalwrt-rockchip-armv8-friendlyarm_nanopc-t4-rootfs.tar.gz --rootfs local:0.5 --ostype unmanaged --hostname ImmortalWrt --arch arm64 --cores 2 --memory 512 --swap 0 -net0 bridge=vmbr0,name=eth0
```