---
layout: post
title: Debian 安装 NTP 服务同步时间并修改时区
date: 2021-04-19 19:25
category: [Linux, 树莓派]
tags: [linux, raspberry-pi, ntp, timezone, debian]
---

安装 NTP 服务的相关包

```bash
sudo apt-get install ntp
```

查看上游时间服务器及相关情况

```bash
$ ntpq -p

     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
 0.debian.pool.n .POOL.          16 p    -   64    0    0.000    0.000   0.001
 1.debian.pool.n .POOL.          16 p    -   64    0    0.000    0.000   0.001
 2.debian.pool.n .POOL.          16 p    -   64    0    0.000    0.000   0.001
 3.debian.pool.n .POOL.          16 p    -   64    0    0.000    0.000   0.001
-ntp7.flashdance 192.36.143.153   2 u    4   64    3  283.451   26.549  13.112
-ntp1.ams1.nl.le 130.133.1.10     3 u    2   64    3  243.497    7.497  18.333
+ntp1.flashdance 192.36.143.130   2 u    -   64    3  258.727   17.178  18.617
*a.chl.la        131.188.3.222    2 u    3   64    3  191.407   13.202  18.098
-ntp5.flashdance 192.36.143.150   2 u    1   64    3  249.094   13.284  15.109
-ntp.xtom.nl     104.63.202.17    2 u    2   64    3  161.752   13.263  17.390
-time.cloudflare 10.71.14.51      3 u    -   64    3  206.584    8.819  16.999

```

将服务器修改为上海时区（CST 时间）

```bash
sudo ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```



### 扩展

Linux 有两个时间来源，分别是硬件时间（CMOS 时间）和软件时间（操作系统时间），通常分别使用 `hwclock` 和 `date` 命令来访问