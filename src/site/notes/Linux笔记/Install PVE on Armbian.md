---
{"dg-publish":true,"permalink":"/Linux笔记/Install PVE on Armbian/","tags":["PVE","Armbian","Linux"],"noteIcon":"","created":"2024-04-24T22:00:12.537+08:00","updated":"2024-05-18T01:35:18.764+08:00"}
---

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
address 192.168.10.109/24
gateway 192.168.10.1
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
127.0.0.1   localhost
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


76:86:BA:56:45:A1

https://www.zhou.pp.ua/2023/08/08/n1/


