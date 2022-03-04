---
layout: post
title: 在 Linux 上查看硬盘 Smart 信息
date: 2022-02-13 13:35
category: Linux
tags: [linux, raspberry-pi]
---

本文将简单介绍如何在 Linux 上使用命令查看硬盘的 SMART 信息。

## 安装

### Debian 系
```bash
apt install smartmontools
```

### Red Hat 系
```bash
yum install smartmontools
```

## 简单使用

|---|---|
|查看全部硬盘|```smartctl --scan```|
|查看硬盘的标识信息|```sudo smartctl --info /dev/sdx```|
|查看硬盘的 SMART 信息|```sudo smartctl -a /dev/sdx```|


## SMART 信息中的 TYPE

`Pre-fail` ：SMART 认为硬盘即将发生故障。
`Old_age` ：SMART 认为这是一个正常的磨损。

