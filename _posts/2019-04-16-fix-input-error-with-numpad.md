---
layout: post
title: 解决使用 SecureCRT/Xshell 连接至 Linux 服务器使用 vim 时小键盘输入乱码的问题
date: 2019-04-16 00:47
category: Linux
tags: [linux, vim, ssh, raspberry-pi]
---

## SecureCRT
Options -> Session Options -> Terminal -> Emulation -> Modes -> Mode switching -> 取消勾选 Enable keypad mode switching

## Xshell
会话管理器 -> 在需要修改的会话上右击 -> 终端 -> VT模式 -> 初始数字键盘模式（DECNKM） -> 设置为普通
![](/assets/2019/01.png)

-----

参考链接：https://vi.stackexchange.com/questions/11581/why-doesnt-my-numpad-work-right-in-my-terminal