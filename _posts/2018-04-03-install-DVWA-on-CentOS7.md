---
layout: post
title: CentOS 7 + DVWA 安装搭建过程
date: 2018-04-03 21:24
category: [网络安全, Linux]
tags: [centos7, dvwa, linux]
---

## 下载

DVWA 的官方网站：http://www.dvwa.co.uk/

DVWA 的 Github 页面：https://github.com/ethicalhack3r/DVWA

可以先从 Windows 上下载后导入 CentOS7

也可以使用命令 `wget https://github.com/ethicalhack3r/DVWA/archive/master.zip` 来下载 DVWA

如有提示 `bash: apt: command not found...` 的，请使用 `yum install wget` 命令安装 wget 工具（ debian 系的 Linux 请使用 `apt install wget` 来安装）

下载完成后，在 Win 下先行解压，或是使用 `unzip DVWA-master.zip` 来获得 DVWA 文件夹，稍后即用

## 运行环境

这里直接使用 LAMP 来达到 Linux + Apache + MySQL + PHP 的环境要求
运行 `wget -c http://soft.vpser.net/lnmp/lnmp1.4.tar.gz && tar zxf lnmp1.4.tar.gz && cd lnmp1.4 && ./install.sh lamp` 一路回车选择默认项，稍等片刻，即可完成安装

也可以参考 [LAMP的官方页面](https://lnmp.org/install.html) 来进行详细的自定义安装

当然手动配置一个符合条件的环境也是完全可以的！

## 安装 DVWA

将之前解压出的 DVWA 文件夹放入 `/home/wwwroot/default/` （ LAMP 默认的网站目录）内

此时访问 http://10.29.219.79/DVWA （我的 CentOS7 主机地址，请访问自己对应主机的IP，下同），会出现如下错误提示

```
DVWA System error - config file not found. Copy config/config.inc.php.dist to config/config.inc.php and configure to your environment.
```

根据提示，我们进入 `/home/wwwroot/default/DVWA/config`，使用 `cp config.inc.php.dist config.inc.php` 将配置文件复制一份，然后输入 `vim config.inc.php` 开始编辑配置文件

```
<?php

# If you are having problems connecting to the MySQL database and all of the variables below are correct
# try changing the 'db_server' variable from localhost to 127.0.0.1. Fixes a problem due to sockets.
#   Thanks to @digininja for the fix.

# Database management system to use
$DBMS = 'MySQL';
#$DBMS = 'PGSQL'; // Currently disabled

# Database variables
#   WARNING: The database specified under db_database WILL BE ENTIRELY DELETED during setup.
#   Please use a database dedicated to DVWA.
#
# If you are using MariaDB then you cannot use root, you must use create a dedicated DVWA user.
#   See README.md for more information on this.
$_DVWA = array();
$_DVWA[ 'db_server' ]   = '127.0.0.1';
$_DVWA[ 'db_database' ] = 'dvwa';
$_DVWA[ 'db_user' ]     = 'root';
$_DVWA[ 'db_password' ] = 'p@ssw0rd';

# Only used with PostgreSQL/PGSQL database selection.
$_DVWA[ 'db_port '] = '5432';

# ReCAPTCHA settings
#   Used for the 'Insecure CAPTCHA' module
#   You'll need to generate your own keys at: https://www.google.com/recaptcha/admin/create
$_DVWA[ 'recaptcha_public_key' ]  = '';
$_DVWA[ 'recaptcha_private_key' ] = '';

# Default security level
#   Default value for the secuirty level with each session.
#   The default is 'impossible'. You may wish to set this to either 'low', 'medium', 'high' or impossible'.
$_DVWA[ 'default_security_level' ] = 'impossible';

# Default PHPIDS status
#   PHPIDS status with each session.
#   The default is 'disabled'. You can set this to be either 'enabled' or 'disabled'.
$_DVWA[ 'default_phpids_level' ] = 'disabled';

# Verbose PHPIDS messages
#   Enabling this will show why the WAF blocked the request on the blocked request.
#   The default is 'disabled'. You can set this to be either 'true' or 'false'.
$_DVWA[ 'default_phpids_verbose' ] = 'false';

?>
```

其中，我们只需要将 `$_DVWA[ 'db_password' ] = 'p@ssw0rd';` 这行的密码修改为我们的 MySQL 使用的默认密码 `root` 即可（如果在安装 LAMP 时选择了其他数据库密码，这里请填写相应的密码）


## 完成安装

完成上述步骤后，访问 http://10.29.219.79/DVWA ，将会被重定向至 http://10.29.219.79/DVWA/setup.php，单击页面底部的 `Create / Reset Database` 按钮，即可跳转至 DVWA 的登陆页面，开始使用吧~



## 额外补充
- 由于目标系统为 Linux 记得在浏览器地址栏输入地址时区分大小写
- DVWA 的默认登陆帐号是 `admin` 密码是 `password`
- 在 `setup.php` 页面上我们仍然会看到几行红字，修复方式见后续文章