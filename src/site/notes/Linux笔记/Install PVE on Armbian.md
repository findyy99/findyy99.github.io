---
{"dg-publish":true,"permalink":"/Linux笔记/Install PVE on Armbian/","noteIcon":"","created":"2024-04-24T22:00:12.537+08:00","updated":"2024-04-27T00:02:50.529+08:00"}
---

76:86:BA:56:45:A1

https://www.zhou.pp.ua/2023/08/08/n1/
1.	Disable `NetworkManager`
```bash
systemctl stop NetworkManager
systemctl disable NetworkManager
```
2. Modified the network config
```bash
vim /etc/network/interfaces 
```
Below is an example:
```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
hwaddress ether fc:7c:02:28:99:0e
# the address and gateway depends on your network
# address is the ip of your armbian device
# gateway is the ip of your router
address 192.168.1.228/24
gateway 192.168.1.1
```
3.	Customize the node name of PVE
```bash
vim /etc/hostname

eg: R08
```
4. Modified the `hosts`
```bash 
vim /etc/hosts

eg:
127.0.0.1   localhost.localdomain localhost
192.168.10.109   R08.proxmox.com R08
::1   localhost ip6-localhost ip6-loopback
fe00::0   ip6-localnet
ff00::0   ip6-mcastprefix
ff02::1   ip6-allnodes
ff02::2   ip6-allrouters

```
5.  Then, you may `reboot` you device.
6.	Backup and renew `debian` source(especially for `CN` users.)
```bash
# Backup the sources.list
mv /etc/apt/sources.list /etc/apt/sources.list.bak
```

```bash
vim /etc/apt/sources.list
```

```bash
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
```

7. Backup and renew `armbian` source(especially for `CN` users.)
*This step is not as same as step `6`.*
```bash
# Backup armbian.list
mv /etc/apt/sources.list.d/armbian.list /etc/apt/sources.list.d/armbian.list.bak
```

```bash
vim /etc/apt/sources.list.d/armbian.list
```

```
deb [signed-by=/usr/share/keyrings/armbian.gpg] https://mirrors.tuna.tsinghua.edu.cn/armbian bookworm main bookworm-utils bookworm-desktop
```
8.	Set the `path` for command
```bash
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```
9. Add `promox` source for `armbian`
```bash
echo "deb https://mirrors.apqa.cn/proxmox/debian/pve bookworm port">/etc/apt/sources.list.d/pveport.list 
```

```file
They are rsync from mirrors.apqa.cn  
Golbal: https://global.mirrors.apqa.cn (Cloudflare)  
Korea: https://mirrors.apqa.cn  
Hong Kong: https://hk.mirrors.apqa.cn  
China: https://mirrors.lierfang.com  
Germany: https://de.mirrors.apqa.cn
```
10. Add trust key for `promox` source
```bash
curl https://mirrors.apqa.cn/proxmox/debian/pveport.gpg -o /etc/apt/trusted.gpg.d/pveport.gpg
```

11. Install PVE
```bash
apt update && apt install proxmox-ve -y
```

If there pops any selection windows, you need to select the first choice.
![armbian - Proxmox Virtual Environment.jpeg](/img/user/Linux%E7%AC%94%E8%AE%B0/assets/armbian%20-%20Proxmox%20Virtual%20Environment.jpeg)
If everything works fine, you will access to your PVE via `https://ip:8006`.
*Note*
If you encounter the following error,
```bash
Errors were encountered while processing:  
pve-manager  
proxmox-ve  
E: Sub-process /usr/bin/dpkg returned an error code (1)
```

Here is a solution.
```bash
rm -f /etc/pve/pve-root-ca.pem /etc/pve/priv/pve-root-ca.* /etc/pve/local/pve-ssl.*

pvecm updatecerts -f

service pveproxy restart|
```


echo "deb https://mirrors.ustc.edu.cn/proxmox/debian/pve bookworm pve-no-subscription" > /etc/apt/sources.list.d/pve-no-subscription.list

echo “deb https://mirrors.apqa.cn/proxmox/debian/pve bookworm port”>/etc/apt/sources.list.d/pveport.list

curl https://mirrors.ustc.edu.cn/proxmox/debian/pve/dists/bookworm/Release.gpg -o /etc/apt/trusted.gpg.d/pve-no-subscription.gpg


curl https://mirrors.apqa.cn/proxmox/debian/pveport.gpg -o /etc/apt/trusted.gpg.d/pveport.gpg


https://www.zhou.pp.ua/2023/08/08/n1/

https://mirrors.apqa.cn/

systemctl stop pve-ha-lrm.service 
systemctl stop pve-ha-crm.service 
systemctl disable pve-ha-lrm.service 
systemctl disable pve-ha-crm.service


systemctl stop pve-firewall.service 
systemctl disable pve-firewall.service

systemctl stop spiceproxy.service 
systemctl disable spiceproxy.service

https://www.spiritlhl.net/guide/pve/pve_custom.html


https://images.linuxcontainers.org/images/

https://github.com/vernesong/OpenClash/releases/tag/v0.46.003-beta

export https_proxy='http://192.168.10.139:8899'
export http_proxy='http://192.168.10.139:8899'
export socks5_proxy='http://192.168.10.139:9988'

option enabled '1' 
option proxy_https 'http://192.168.10.139:8899'



iptables -t nat -A PREROUTING -i ztk4jp2wmc -p tcp --dport 8080 -j DNAT --to-destination 192.168.10.182:80
iptables -A FORWARD -i ztk4jp2wmc -d 192.168.10.182 -p tcp --dport 8080 -j ACCEPT


# 将从 ZeroTier 网络接收到的 TCP 80 端口流量转发到虚拟机 192.168.10.182 的 TCP 80 端口
iptables -t nat -A PREROUTING -i ztk4jp2wmc -p tcp --dport 8001 -j DNAT --to-destination 192.168.10.182:80

# 允许转发规则通过
iptables -A FORWARD -i ztk4jp2wmc -d 192.168.10.182 -p tcp --dport 80 -j ACCEPT
curl -v https://gh.findyy.workers.dev/https://github.com/xiaorouji/openwrt-passwall/releases/download/4.77-4/passwall_packages_ipk_aarch64_generic.zip


```bash
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:29287#%E8%B7%9D%E7%A6%BB%E4%B8%8B%E6%AC%A1%E9%87%8D%E7%BD%AE%E5%89%A9%E4%BD%99%EF%BC%9A25%20%E5%A4%A9
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:29287#%E5%A5%97%E9%A4%90%E5%88%B0%E6%9C%9F%EF%BC%9A2024-11-20
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:29287#%F0%9F%87%BA%F0%9F%87%B8ss%E7%BE%8E%E5%9B%BD0%7C%E2%91%A0%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:13410#%F0%9F%87%BA%F0%9F%87%B8ss%E7%BE%8E%E5%9B%BD1%7C%E2%91%A0%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@tj-lt_ssr.coderfan.org:29997#%F0%9F%87%BA%F0%9F%87%B8ss%E7%BE%8E%E5%9B%BD2%7C%E2%91%A0%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@tj-lt_ssr.coderfan.org:23872#%F0%9F%87%AF%F0%9F%87%B5ss%E6%97%A5%E6%9C%AC0%7C%E2%91%A1%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@tj-lt_ssr.coderfan.org:47498#%F0%9F%87%AF%F0%9F%87%B5ss%E6%97%A5%E6%9C%AC1%7C%E2%91%A1%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:45242#%F0%9F%87%AF%F0%9F%87%B5ss%E6%97%A5%E6%9C%AC2%7C%E2%91%A1%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:18552#%F0%9F%87%AF%F0%9F%87%B5ss%E6%97%A5%E6%9C%AC3%7C%E2%91%A1%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:40887#%F0%9F%87%AD%F0%9F%87%B0ss%E9%A6%99%E6%B8%AF0%7C%E2%91%A1%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@tj-lt_ssr.coderfan.org:40651#%F0%9F%87%AD%F0%9F%87%B0ss%E9%A6%99%E6%B8%AF1%7C%E2%91%A1%E5%80%8D%E7%8E%87-NetflixUnblock
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:51594#%F0%9F%87%AD%F0%9F%87%B0ss%E9%A6%99%E6%B8%AF2%7C%E2%91%A1%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:15317#%F0%9F%87%AD%F0%9F%87%B0ss%E9%A6%99%E6%B8%AF3%7C%E2%91%A1%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:49146#%F0%9F%87%AD%F0%9F%87%B0ss%E9%A6%99%E6%B8%AF4%7C%E2%91%A1%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@tj-lt_ssr.coderfan.org:13138#%F0%9F%87%B8%F0%9F%87%ACss%E6%96%B0%E5%8A%A0%E5%9D%A10%7C%E2%91%A1%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@tj-lt_ssr.coderfan.org:34774#%F0%9F%87%B8%F0%9F%87%ACss%E6%96%B0%E5%8A%A0%E5%9D%A11%7C%E2%91%A1%E5%80%8D%E7%8E%87-NetflixUnblock
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:24571#%F0%9F%87%B8%F0%9F%87%ACss%E6%96%B0%E5%8A%A0%E5%9D%A12%7C%E2%91%A1%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:44023#%F0%9F%87%A9%F0%9F%87%AAss%E5%BE%B7%E5%9B%BD%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:42469#%F0%9F%87%AB%F0%9F%87%AEss%E8%8A%AC%E5%85%B0%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@tj-lt_ssr.coderfan.org:37009#%F0%9F%87%A8%F0%9F%87%A6ss%E5%8A%A0%E6%8B%BF%E5%A4%A7%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:47579#%F0%9F%87%B5%F0%9F%87%B1ss%E6%B3%A2%E5%85%B0%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:21968#%F0%9F%87%B9%F0%9F%87%BCss%E5%8F%B0%E6%B9%BE0%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@tj-lt_ssr.coderfan.org:16465#%F0%9F%87%B9%F0%9F%87%BCss%E5%8F%B0%E6%B9%BE1%7C%E2%91%A4%E5%80%8D%E7%8E%87-NetflixUnblock
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:23448#%F0%9F%87%B5%F0%9F%87%B0ss%E5%B7%B4%E5%9F%BA%E6%96%AF%E5%9D%A6%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:48053#%F0%9F%87%A6%F0%9F%87%B7ss%E9%98%BF%E6%A0%B9%E5%BB%B7%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@tj-lt_ssr.coderfan.org:13851#%F0%9F%87%B3%F0%9F%87%ACss%E5%B0%BC%E6%97%A5%E5%88%A9%E4%BA%9A%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:17267#%F0%9F%87%AB%F0%9F%87%B7ss%E6%B3%95%E5%9B%BD%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:54370#%F0%9F%87%B3%F0%9F%87%B1ss%E8%8D%B7%E5%85%B0%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:11961#%F0%9F%87%BF%F0%9F%87%A6ss%E5%8D%97%E9%9D%9E%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:31276#%F0%9F%87%AE%F0%9F%87%B9ss%E6%84%8F%E5%A4%A7%E5%88%A9%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:52573#%F0%9F%87%B9%F0%9F%87%B7ss%E5%9C%9F%E8%80%B3%E5%85%B6%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@jp-zj_ssr.coderfan.org:51826#%F0%9F%87%AE%F0%9F%87%B3ss%E5%8D%B0%E5%BA%A6%7C%E2%91%A4%E5%80%8D%E7%8E%87
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@sg6-web1.breakwalls.us:55555#%F0%9F%87%B8%F0%9F%87%ACss%E6%96%B0%E5%8A%A0%E5%9D%A1%7C%E2%91%A1%E5%80%8D%E7%8E%87-%E7%B4%A7%E6%80%A5%E5%A4%87%E7%94%A8
ss://YWVzLTI1Ni1nY206OTg3YmUxZTItYzAwNS00ZDRhLThhNDEtZDRmODUxNmY4Y2U5@hk6-web1.breakwalls.us:55555#%F0%9F%87%AD%F0%9F%87%B0ss%E9%A6%99%E6%B8%AF%7C%E2%91%A1%E5%80%8D%E7%8E%87-%E7%B4%A7%E6%80%A5%E5%A4%87%E7%94%A8

```


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


src/gz openwrt_core https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/23.05.3/targets/armsr/armv8/packages

src/gz openwrt_base https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/23.05.3/packages/aarch64_generic/base

src/gz openwrt_luci https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/23.05.3/packages/aarch64_generic/luci

src/gz openwrt_packages https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/23.05.3/packages/aarch64_generic/packages

src/gz openwrt_routing https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/23.05.3/packages/aarch64_generic/routing

src/gz openwrt_telephony https://mirrors.tuna.tsinghua.edu.cn/openwrt/releases/23.05.3/packages/aarch64_generic/telephon


pct create 102 /mnt/KingSton/template/cache/immortalwrt-rockchip-armv8-friendlyarm_nanopc-t4-rootfs.tar.gz --ostype unmanaged --hostname ImmortalWrt --arch arm64 --cores 2 --memory 512 --swap 0 -net0 bridge=vmbr0,name=eth0