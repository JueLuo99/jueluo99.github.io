---
layout: post
title: 在 Kali Linux 下安装 vmtools
date: 2017-09-28 08:18
category: 网络安全
tags: [kali, vmtools, virtualization]
---

在使用 VMware Workstion 自带的 vmtools 安装失败后，在官网上找到了官方推荐的安装方法（https://www.kali.org/news/kali-linux-rolling-edition-2016-1/）

（可选）配置 apt 源，将 ```/etc/apt/sources.list``` 这个 apt 安装源修改为
```
#中科大kali源
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main contrib non-free
#或是
#阿里云kali源
#deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
#deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
#deb http://mirrors.aliyun.com/kali-security kali-rolling/updates main contrib non-free
```

执行如下命令
```
apt update
apt install open-vm-tools-desktop fuse
reboot
```

重启完毕后，安装完成