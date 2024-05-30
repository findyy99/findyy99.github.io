---
{"dg-publish":true,"permalink":"/Linux笔记/Custom PVE/","noteIcon":"","created":"2024-05-13T22:39:12.341+08:00","updated":"2024-05-19T15:10:05.516+08:00"}
---

```
systemctl stop pve-ha-lrm.service 
systemctl stop pve-ha-crm.service 
systemctl disable pve-ha-lrm.service
systemctl disable pve-ha-crm.service
```


```
systemctl stop pve-firewall.service 
systemctl disable pve-firewall.service
```

```
systemctl stop spiceproxy.service 
systemctl disable spiceproxy.service
```

https://www.spiritlhl.net/guide/pve/pve_custom.html