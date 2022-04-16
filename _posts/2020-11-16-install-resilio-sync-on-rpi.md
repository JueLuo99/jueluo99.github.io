---
layout: post
title: 树莓派安装 Resilio Sync
date: 2020-11-16 18:23
category: 树莓派
tags: [raspberry-pi]
---

## 注册 Resilio 存储库

创建文件 `/etc/apt/sources.list.d/resilio-sync.list` 并写入下面内容来注册 Resilio 存储库：

```sh
echo "deb http://linux-packages.resilio.com/resilio-sync/deb resilio-sync non-free" | sudo tee /etc/apt/sources.list.d/resilio-sync.list
```

## 添加公钥

下载 Resilio 软件源公钥并添加到 apt 信任列表：

```sh
curl -LO http://linux-packages.resilio.com/resilio-sync/key.asc && sudo apt-key add ./key.asc
```


## 安装 Resilio Sync 套件

使用下面命令安装：

```sh
sudo apt-get update 
sudo apt-get install resilio-sync
```

## 使用方法
输入 `sudo service resilio-sync start` 启动 Resilio Sync

浏览器使用 IP 加端口号即可进入管理页面，默认端口号为 `8888`

## 开机启动

使用 `sudo systemctl enable resilio-sync` 即可

## 参考资料

官方手册：https://help.resilio.com/hc/en-us/articles/204762449-Guide-to-Linux