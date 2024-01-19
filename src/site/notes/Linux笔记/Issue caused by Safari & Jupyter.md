---
{"dg-publish":true,"permalink":"/Linux笔记/Issue caused by Safari & Jupyter/","tags":["Linux","Jupyter","Safari","macOS"]}
---

今天，搭建了一个远程的Jupyter服务器，这玩意用Safari打开，一直报错404，给搞麻了；后面换了Chrome，一切OK。
```bash 
[W 2024-01-10 06:12:38.774 ServerApp] 404 GET ws://xxxx:8889/api/kernels/86d332d7-6158-49d0-a0e9-212e01cdd79b/channels?session_id=491d7cc6-0c1e-4ac7-b5bf-915f7f37981a (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 0.92ms referer=None
[W 2024-01-10 06:12:39.150 ServerApp] 404 GET ws://xxxxx:8889/api/kernels/86d332d7-6158-49d0-a0e9-212e01cdd79b/channels?session_id=491d7cc6-0c1e-4ac7-b5bf-915f7f37981a (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 1.09ms referer=None
[W 2024-01-10 06:12:40.136 ServerApp] 404 GET ws://xxxxx:8889/api/events/subscribe (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 1.10ms referer=None
[W 2024-01-10 06:12:40.719 ServerApp] 404 GET ws://xxxxx:8889/terminals/websocket/1 (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 1.23ms referer=None
[W 2024-01-10 06:12:40.848 ServerApp] 404 GET ws://xxxxx:8889/api/kernels/86d332d7-6158-49d0-a0e9-212e01cdd79b/channels?session_id=f0c4b3b4-387d-4b43-9a4a-7cc897d7ce5c (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 0.99ms referer=None
[W 2024-01-10 06:12:41.432 ServerApp] 404 GET ws://xxxxx:8889/api/events/subscribe (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 1.01ms referer=None
[W 2024-01-10 06:12:41.569 ServerApp] 404 GET ws://xxxxx:8889/api/kernels/86d332d7-6158-49d0-a0e9-212e01cdd79b/channels?session_id=491d7cc6-0c1e-4ac7-b5bf-915f7f37981a (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 1.06ms referer=None
[W 2024-01-10 06:12:42.608 ServerApp] 404 GET ws://xxxxx:8889/api/kernels/86d332d7-6158-49d0-a0e9-212e01cdd79b/channels?session_id=f0c4b3b4-387d-4b43-9a4a-7cc897d7ce5c (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 1.13ms referer=None
[W 2024-01-10 06:12:44.401 ServerApp] 404 GET ws://xxxxx:8889/api/events/subscribe (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 1.15ms referer=None
[W 2024-01-10 06:12:45.005 ServerApp] 404 GET ws://xxxxx:8889/terminals/websocket/1 (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 0.78ms referer=None
[W 2024-01-10 06:12:45.354 ServerApp] 404 GET ws://xxxxx:8889/api/kernels/86d332d7-6158-49d0-a0e9-212e01cdd79b/channels?session_id=491d7cc6-0c1e-4ac7-b5bf-915f7f37981a (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 1.09ms referer=None
[W 2024-01-10 06:12:46.965 ServerApp] 404 GET ws://xxxxx:8889/api/events/subscribe (71d61e3e104548e0aa3714a146ca00c2@219.157.128.206) 1.12ms referer=None
```