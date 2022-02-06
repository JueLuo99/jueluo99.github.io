---
layout: post
title: 使用 GitHub Desktop 来同步码云上的项目
date: 2017-03-09 23:41
category: Git
tags: [git, github, gitee]
---

首先运行 Git Shell，GitHub Desktop 安装时应该已经附带了 Git Shell

默认会使用以前 Clone 时使用的路径，如果需要更改，使用如下命令：
```
cd *:\（你需要的路径）
```
使用如下命令将码云上的项目 Clone 至本地：
```
git clone https://git.oschina.net/码云上项目的地址.git
```
私有项目会要求输入用于登陆码云的邮箱及密码（此处注意，你输入的密码是不会有任何显示的）：
```
Cloning into '项目名'...
Username for 'https://git.oschina.net': //此处输入邮箱
Password for 'https://你输入的邮箱@git.oschina.net'://此处输入密码
```
输入正确无误后就会开始 Clone，等待 Clone 完成即可

Clone 完成后，关闭 Git Shell，打开 GitHub Desktop

![](/assets/2017/01.png)

点击左上角加号，选择 add，填入刚刚 Clone 的目录，选择“Add repository”

左侧 repo 列表内就会出现需要的项目，可以使用 Sync 功能正常同步至码云