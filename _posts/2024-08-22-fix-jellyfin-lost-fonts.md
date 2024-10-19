---
layout: post
title: 快速解决 Docker Compose 部署的 Jellyfin 更新后文本变成方框
date: 2024-08-22 20:21
category: Docker
tags: [docker, docker-compose, jellyfin, linux]
---

我使用 Docker Compose 部署的 Jellyfin，每次执行 `docker-compose pull` 更新后，就会因为缺失汉字字体而导致部分中文变为方框

解决方法很简单，只需要安装 `fonts-noto-cjk-extra` 这个包即可

但受限于国内网络状况，想要更高效地完成这项工作，还需要替换下载源

进入容器后，执行以下命令（使用上海交通大学的镜像源）：

```bash
sed -i "s|http://deb.debian.org/debian|http://mirror.sjtu.edu.cn/debian|g" /etc/apt/sources.list.d/debian.sources && apt update && apt install -y fonts-noto-cjk-extra
```

安装完毕后，**重启该容器**即可


### 参考
1. [Integrate CJK fonts · Issue #161 · linuxserver/docker-jellyfin](https://github.com/linuxserver/docker-jellyfin/issues/161)
1. [上海交通大学 Linux 用户组 软件源镜像服务](https://mirror.sjtu.edu.cn/docs/debian)