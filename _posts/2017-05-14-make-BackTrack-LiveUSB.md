---
layout: post
title: 将 BackTrack 制作为 LiveUSB
date: 2017-05-14 21:30
category: 网络安全
tags: [linux, backtrack, liveusb]
---

本文将介绍如何把 BackTrack 制作为一个可以从 U 盘启动的 LiveUSB 系统

## 准备所需工具

### unetbootin

GitHub 地址：https://github.com/unetbootin/unetbootin/

用于将下载的 iso 镜像写入至U盘，自带简中

### BackTrack 镜像

这里使用的是 BackTrack 的最后一个发布版 BackTrack 5 R3 
下载地址引用自官网（www.backtrack-linux.org）
- [BT5R3-GNOME-64.torrent](http://www.backtrack-linux.org/torrents/BT5R3-GNOME-64.torrent)
- [BT5R3-GNOME-32.torrent](http://www.backtrack-linux.org/torrents/BT5R3-GNOME-32.torrent)
- [BT5R3-KDE-64.torrent](http://www.backtrack-linux.org/torrents/BT5R3-KDE-64.torrent)
- [BT5R3-KDE-32.torrent](http://www.backtrack-linux.org/torrents/BT5R3-KDE-32.torrent)
- [BT5R3-GNOME-32-VM.torrent](http://www.backtrack-linux.org/torrents/BT5R3-GNOME-32-VM.torrent)

种子内包含了一个用于校验 iso 镜像 MD5 值的一个 txt 文件

## 开始制作

1. 插入U盘（如果先打开了 unetbootin 再插入U盘将会识别不到）
1. 打开 unetbootin 选择使用“光盘镜像”并将路径指向到自己下载的镜像所在的地址。
    - “用于在重启之间保留文件的空间”可以填写一个适当的数值，以用于保存运行时创建的文件。若填写为“0”则每次重新退出系统后将不会保留任何对系统所做的更改。
    - 最下方的“类型”选择“USB 驱动器”并指向自己所用U盘的驱动器号
![](/assets/2018/01.png)
1. 点击“确定”开始制作，等待制作完成。
![](/assets/2018/02.png)

## 测试

1. 从 boot 菜单选择U盘启动
1. 在 BackTrack5 的系统启动界面，选择“Default”项进入系统
![](/assets/2018/03.png)
1. 等待启动完毕后，在命令行输入“stratx”进入桌面模式![](/assets/2018/04.png)值得一提的是，我在实际操作过程中并没有被要求输入登陆Linux的账号和密码