---
layout: post
title: DVWA + LAMP 安装完成后的最后调整
date: 2018-04-03 22:19
category: 网络安全
tags: [dvwa, lamp, php, linux]
---

使用 LAMP 的默认配置搭建 DVWA 后可能仍然会在 `setup.php` 页面上见到数行红字，这里简单描述下解决方法

## PHP function allow_url_include: Disabled

如果不修复此项，在使用 File Inclusion 模块时会出现 `The PHP function allow_url_include is not enabled.` 的错误提示

修复方式：

使用 `vim /usr/local/php/etc/php.ini` 命令打开配置文件
（别的运行环境请使用 `find / -name php.ini` 命令找到配置文件）

在 vim 内摁下 Shift + : 输入 `/allow_url_include` 回车搜索

将 `allow_url_include = Off` 的参数改为 `on`

`service httpd restart` 重启 Apache

## reCAPTCHA key: Missing

谷歌验证码的功能不可用，考虑到我国🤔国情，修复了也没什么用

修复方式：

前往 https://www.google.com/recaptcha/admin#list 根据页面提示申请一个 key，并将申请获得的 key 填入 DVWA 的配置文件 config.inc.php 内