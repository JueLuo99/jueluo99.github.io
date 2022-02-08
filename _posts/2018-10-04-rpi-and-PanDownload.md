---
layout: post
title: 搭建树莓派+PanDownload(aria2)远程下载器
date: 2018-10-04 19:38
category: [树莓派, Linux] 
tags: [raspberry-pi, linux, aria2]
---

在下载百度云盘的内容时，偶然发现 [PanDownload](https://pandownload.com) 拥有一个远程下载的功能，于是萌生了利用闲置树莓派作为下载机长时间开机下载的想法。

<!-- more -->


1. 安装 aria2

    ```
    sudo apt install aria2
    ```
    确认安装，等待安装完成

2. 创建 aria2 的配置文件

    ```
    vim touch /etc/aria2/aria2.conf
    ```
    
    这里从网上找了一份配置文件并根据自己的需要稍加修改
    
    ```
    ## 文件保存相关 ##
    # 文件保存目录
    dir=/mnt/storage/download
    # 启用磁盘缓存, 0为禁用缓存, 需1.16以上版本, 默认:16M
    disk-cache=32M
    # 断点续传
    continue=true
    # 文件预分配方式, 能有效降低磁盘碎片, 默认:prealloc
    # 预分配所需时间: none < falloc ? trunc < prealloc
    # falloc和trunc则需要文件系统和内核支持
    # NTFS建议使用falloc, EXT3/4建议trunc, MAC 下需要注释此项
    #file-allocation=falloc

    ## 下载连接相关 ##
    # 最大同时下载任务数, 运行时可修改, 默认:5
    #max-concurrent-downloads=5
    # 同一服务器连接数, 添加时可指定, 默认:1
    max-connection-per-server=16
    # 整体下载速度限制, 运行时可修改, 默认:0（不限制）
    #max-overall-download-limit=0
    # 单个任务下载速度限制, 默认:0（不限制）
    #max-download-limit=0
    # 整体上传速度限制, 运行时可修改, 默认:0（不限制）
    #max-overall-upload-limit=0
    # 单个任务上传速度限制, 默认:0（不限制）
    #max-upload-limit=0
    # 禁用IPv6, 默认:false
    disable-ipv6=true
    # 最小文件分片大小, 添加时可指定, 取值范围 1M -1024M , 默认：20M
    # 假定 size=10M , 文件为 20MiB 则使用两个来源下载; 文件为 15MiB 则使用一个来源下载
    min-split-size=10M
    # 单个任务最大线程数, 添加时可指定, 默认:5
    #split=10
    
    ## 进度保存相关 ##
    # 从会话文件中读取下载任务
    input-file=/etc/aria2/aria2.session
    # 在Aria2退出时保存错误的、未完成的下载任务到会话文件
    save-session=/etc/aria2/aria2.session
    # 定时保存会话, 0为退出时才保存, 需1.16.1以上版本, 默认:0
    save-session-interval=150
    
    ## RPC相关设置 ##
    # 启用RPC, 默认:false
    enable-rpc=true
    # 允许所有来源, 默认:false
    rpc-allow-origin-all=true
    # 允许外部访问, 默认:false
    rpc-listen-all=true
    # RPC端口, 仅当默认端口被占用时修改
    rpc-listen-port=6800
    # 设置的RPC授权令牌, v1.18.4新增功能, 取代 --rpc-user 和 --rpc-passwd 选项
    rpc-secret=yourpasswordhere

    ## BT/PT下载相关 ##
    # 当下载的是一个种子(以.torrent结尾)时, 自动开始BT任务, 默认:true
    #follow-torrent=true
    # 客户端伪装, PT需要
    peer-id-prefix=-TR2770-
    user-agent=Transmission/2.77
    # 强制保存会话, 即使任务已经完成, 默认:false
    # 较新的版本开启后会在任务完成后依然保留.aria2文件
    #force-save=false
    # 继续之前的BT任务时, 无需再次校验, 默认:false
    bt-seed-unverified=true
    # 保存磁力链接元数据为种子文件(.torrent文件), 默认:false
    bt-save-metadata=true
    ```

    记得注意这个文件中的 下载目录 和 令牌 要根据自己的需要填写（不想使用令牌的可以将那行注释）

3. 写一个启动 aria2 的脚本（可选）
    
    用于在 aria2 没有启动时更方便地启动服务
    ```
    vim runAria2.sh
    ```

    写入如下内容
    ```
    aria2c --conf-path=/root/aria2_config
    ```

    尝试执行
    ```
    ./runAria2.sh
    ```
    运行正确将不会有任何提示

4. 使用网页监控 aria2 下载状况（可选）

    我已经安装过 Nginx 和 git 两个功能了，如果没有，执行以下步骤依次安装
    ```
    apt install -y nginx git
    ```

    这里选择了一个自带多语言的 github 项目作为 WebUI
    ```
    #只能 clone 到空目录，所以先清空默认网页根目录下的文件
    rm -rf /var/www/html
    git clone https://github.com/ziahamza/webui-aria2.git /var/www/html
    ```

5. 配置 Pandownload 下载

    远程页面设置如下图，填写 IP 和上面配置文件里所设定的端口 6800 即可
    
    token 部分填写的是上面配置文件中所写的令牌

    ![设置页面](/assets/2018/21.png)

    选择需要下载文件后，弹出选择下载路径窗口，填写需要的下载路径即可

    ![选择下载路径](/assets/2018/22.png)

    如果提示“下载失败：无法创建文件”

    ![提示没有权限](/assets/2018/23.png)

    给予所有用户下载目录的写权限即可
    ```
    chmod 777 /mnt/download
    ```

--------

至此，树莓派搭配 Pandownload 的下载组合已经搭建完毕，可以方便地将视频等资料远程下载至树莓派中。

再搭配 samba 等服务，即可随时随地播放下载至树莓派中的媒体文件。

