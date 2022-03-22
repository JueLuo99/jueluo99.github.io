---
layout: post
title: 树莓派禁用 IPv6（Debian8 适用）
date: 2020-11-16 18:01
category: [Linux, 树莓派]
tags: [linux, raspberry-pi, ipv6]
---

1. 使用 `ifconfig` 命令查看是否拥有 IPv6 地址，`inet6 addr` 开头的这一行即为 IPv6 地址

   ```bash
   Link encap: Ethernet Hwaddr a4: 17:31:f5:24:C4
   inet addr: 192.168.1.101 Bcast: 192.168.1.255 Mask:255.255.255.0
   inet6 addr: fe80: :a617:31ff:fef5:24C4/64 Scope:Link
   UP BROADCAST RUNNING MULTICAST MTU: 1500 Metric: 1
   ``` 

1. 编辑 `/etc/sysctl.conf` 文件（需要 root 权限），添加如下内容

   ```bash
   # disable IPv6
   net.ipv6.conf.all.disable_ipv6 = 1
   net.ipv6.conf.default.disable_ipv6 = 1
   net.ipv6.conf.lo.disable_ipv6 = 1
   ```

1. 重新加载 `/etc/sysctl.conf` 配置文件

   ```bash
   sudo sysctl -p
   ```

1. 再次使用 ifconfig 命令检查 IPv6，可以看到已经没有 IPv6 地址