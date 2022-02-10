---
layout: post
title: 解决树莓派初始不支持读写 exFAT 文件系统的问题
date: 2019-06-04 04:39
category: Linux
tags: [linux, raspberry-pi, exfat]
---

挂载文件系统为```exfat```的U盘时提示：
```mount: unknown filesystem type 'exfat'```

运行如下命令后，尝试重新挂载：
```sudo apt install exfat-utils```

