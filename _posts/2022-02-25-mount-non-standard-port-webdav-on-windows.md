---
layout: post
title: 在 Windows 上挂载非标准端口的 WebDAV
date: 2022-02-25 23:23
category: Windows
tags: [webdav, windows]
---

无法在可视化的界面上完成此操作

可以在命令行里使用以下命令实现

```powershell
net use * https://example.com:9001/dav.php
```

挂载成功后，可以至“我的电脑”中修改其显示的名称

*以此法挂载的 WebDAV 服务不能正确显示容量*