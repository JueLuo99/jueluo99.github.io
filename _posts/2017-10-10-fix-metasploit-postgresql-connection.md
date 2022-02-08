---
layout: post
title: Metasploit 没有自动连接 postgresql 数据库的解决方法
date: 2017-10-10 09:48
category: 网络安全
author: tags: [metasploit, postgresql, kali, backtrack5]
---

启动 metasploit 后，发现没有自动连接 postgresql 数据库

- 连接的命令为 `db_connect 用户名:密码@ip/数据库名`

- 连接默认数据库的命令为 `db_connect msf3:toor@127.0.0.1/msf3`


如果还是无法连接，则尝试以下步骤

1. 使用 `service postgresql status` 查看并确保 postgresql 服务已经启动，然后使用 `su postgres` 命令切换到 postgre 账户


2. 使用 `createuser msf3 –P` 命令创建一个 postgresql 数据库账户<br/>
命令中的msf3是要创建的用户名，-P 表示立即给角色指定一个口令<br/>
接下来根据提示输入两次，此次使用 `toor` 作为密码

3. 使用 `createdb --owner=msf3 msf3` 创建数据库<br/>
owner参数表示数据库的所有者，此次指定给刚刚创建的msf3，最后一个“msf3”表示数据库的名称

4. 使用 `exit` 命令退出当前用户，回到 root 用户手动连接的步骤<br/>
再次尝试 `db_connect msf3:msf@localhost/msf3`
