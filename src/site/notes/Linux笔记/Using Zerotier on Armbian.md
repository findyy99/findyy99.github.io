---
{"dg-publish":true,"permalink":"/Linux笔记/Using Zerotier on Armbian/","tags":["Zerotier","Armbian","Linux"],"noteIcon":"","created":"2024-05-13T22:41:28.220+08:00","updated":"2024-05-30T22:02:40.392+08:00"}
---


```bash
iptables -t nat -A PREROUTING -i ztk4jp2wmc -p tcp --dport 8080 -j DNAT --to-destination 192.168.10.182:80
iptables -A FORWARD -i ztk4jp2wmc -d 192.168.10.182 -p tcp --dport 8080 -j ACCEPT
```



# 将从 ZeroTier 网络接收到的 TCP 80 端口流量转发到虚拟机 192.168.10.182 的 TCP 80 端口
```bash
iptables -t nat -A PREROUTING -i ztk4jp2wmc -p tcp --dport 8001 -j DNAT --to-destination 192.168.10.182:80
```

# 允许转发规则通过
```bash
iptables -A FORWARD -i ztk4jp2wmc -d 192.168.10.182 -p tcp --dport 80 -j ACCEPT
```


https://www.neko7ina.com/3pYN3eLUDHwEYg.html