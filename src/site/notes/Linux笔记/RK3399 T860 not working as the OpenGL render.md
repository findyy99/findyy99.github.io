---
{"dg-publish":true,"permalink":"/Linux笔记/RK3399 T860 not working as the OpenGL render/","tags":["Linux","Armbian","RK3399","Panfrost","Mesa"],"noteIcon":"","created":"2024-05-18T00:40:15.576+08:00","updated":"2024-05-18T15:59:03.351+08:00"}
---






strace -f -e trace=file,open,openat -o strace_output.txt glxinfo -B

/dev/dri/renderD128

sudo usermod -a -G render findyy
