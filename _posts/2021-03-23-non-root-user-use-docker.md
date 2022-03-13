---
layout: post
title: 让非 root 用户使用 docker
date: 2021-03-23 20:20
category: [Linux, Docker]
tags: [linux, docker]
---

将当前用户加入 docker 组

```bash
sudo gpasswd -a ${USER} docker
```

重新启动 docker 服务

```bash
sudo systemctl restart docker
```

重新登录该用户即可使用