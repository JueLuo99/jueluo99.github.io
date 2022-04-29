---
layout: post
title: 在 Windows Terminal 中直接打开具有管理员权限的选项卡
date: 2021-04-16 13:55
category: Windows
tags: [windows, terminal, wt]
---

### 思路

在 Linux 下可以使用 `sudo` 命令来直接提升权限，但是在 Windows 下却没有这样的命令行工具

故选择开源工具 `gsudo` 来实现类似功能

### 步骤

1. 安装 `gsudo` 直接使用 PowerShell 进行安装

   ```powershell
   PowerShell -Command "Set-ExecutionPolicy RemoteSigned -scope Process; iwr -useb <https://raw.githubusercontent.com/gerardog/gsudo/master/installgsudo.ps1> | iex"
   ```
1. 根据自身需要选择是否将 `sudo` 作为别名
![Snipaste_2021-04-16_13-27-31.png][1]
1. 打开 Windows Terminal 设置页面，点击左侧“新增”，右侧内容如图填写
![Snipaste_2021-04-16_13-51-39.png][2]
1. 尝试新建选项卡，已可创建具有管理员权限的 PowerShell 选项卡


### 缺点

以此法创建的新选项卡仍然会有 UAC 弹框，但双手不用离开键盘即可继续操作

### 参考

1. [https://github.com/gerardog/gsudo](https://github.com/gerardog/gsudo)
2. [https://blog.poychang.net/run-windows-terminal-as-administrator-with-elevated-admin-permissions/](https://blog.poychang.net/run-windows-terminal-as-administrator-with-elevated-admin-permissions/)


  [1]: /assets/2020/021.png
  [2]: /assets/2020/022.png