---
{"dg-publish":true,"permalink":"/Linux笔记/SSH Things/","tags":["ssh","Linux"]}
---

## Map the remote port to local
```bash
ssh -L53682:localhost:53682 ubuntu@158.101.140.179
```
## Transfer file using scp

```bash
scp -O -i xxxx.pem user@ip:/xx/xx/xx/xxx.ipynb ~/Desktop/xxxx.ipynb
```
