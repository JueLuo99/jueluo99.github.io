---
layout: post
title: 修复 Ubuntu 上 Firefox 中文显示不正确的问题
date: 2021-12-13 08:57
category: Linux
tags: [linux, ubuntu, firefox, server]
---

我使用的是 Ubuntu Server 20.04 LTS，在安装 Firefox 后，通过 X server 启动 Firefox，发现中文字体显示不正确


执行以下命令后，重启 Firefox。即可解决问题

```sh
sudo apt-get install ttf-wqy-microhei  #文泉驿-微米黑
sudo apt-get install ttf-wqy-zenhei  #文泉驿-正黑
sudo apt-get install xfonts-wqy #文泉驿-点阵宋体
```