---
layout: post
title: 如何在 BackTrack5 下安装 Metasploit
date: 2017-03-15 19:47
category: 网络安全
tags: [backtrack5, metasploit, linux]
---

其实 BT5 和 Kali 都自带了这玩意儿......

## 下载

- [Windows 64bit](http://downloads.metasploit.com/data/releases/metasploit-latest-windows-installer.exe)
- [Windows 32bit](http://downloads.metasploit.com/data/releases/metasploit-latest-windows-installer.exe)
- [Linux 64bit](http://downloads.metasploit.com/data/releases/metasploit-latest-linux-x64-installer.run)
- [Linux 32bit](http://downloads.metasploit.com/data/releases/metasploit-latest-linux-installer.run)

## 安装

1. 在任意 Shell 下输入 ` chmod +x ./安装文件.run` 来为“安装文件.run”增加“执行”权限

1. 输入 `./安装文件.run` 来启动安装程序

![图形化安装界面](/assets/2018/11.png)
![同意用户协议](/assets/2018/12.png)
![选择安装路径](/assets/2018/13.png)