---
{"dg-publish":true,"permalink":"/Linux笔记/Linux enable and disable swap/","tags":["Linux"],"noteIcon":"","created":"2024-01-29T16:56:32.806+08:00","updated":"2024-01-29T17:05:30.147+08:00"}
---

# 1.  Enable Swap
## 1.1 Check the usage of Swap
```bash
               total        used        free      shared  buff/cache   available
Mem:             417         188          21           2         221         229
Swap:           2047           0        2047
```
## 1.2 Add Swap file
```bash
cd /usr
mkdir swap && cd swap
dd if=/dev/zero of=/usr/swap/swapfile1 bs=1M count=2048
```
`bs=1M means the size of block written is 1M，count=2048 means we created a swap file which is 2048M totally.`
## 1.3 Check the size of swap file created
```bash
du -sh /usr/swap/swapfile1
```
## 1.4 Make the swap file to be recognized by system
```bash
mkswap /usr/swap/swapfile1
```
## 1.5 Enable usage of the swap file
```bash
swapon /usr/swap/swapfile1
```
## 1.6 Edit `/etc/fstab`
```bash
/usr/swap/swapfile1 swap swap defaults 0 0
```
## 1.7 Check the swap file mounted successfully
```bash
swapon -s
```

Reference:
[1]:https://timberkito.com/?p=98