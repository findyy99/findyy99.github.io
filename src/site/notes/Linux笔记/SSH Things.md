---
{"dg-publish":true,"permalink":"/Linux笔记/SSH Things/","tags":["ssh","Linux"],"noteIcon":"","created":"2022-10-27T14:28:51.344+08:00","updated":"2024-01-19T19:49:03.315+08:00"}
---

## Map the remote port to local
```bash
ssh -L53682:localhost:53682 ubuntu@158.101.140.179
```
## Transfer file using scp

```bash
scp -O -i xxxx.pem user@ip:/xx/xx/xx/xxx.ipynb ~/Desktop/xxxx.ipynb
```
