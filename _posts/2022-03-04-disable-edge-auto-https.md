---
layout: post
title: 禁止 Edge 浏览器自动使用 HTTPS
date: 2022-03-04 20:53
category: Windows
tags: [windows, edge, android]
---

Edge 浏览器会自动套用 HTTPS，但这对开发者来说是不友好的。

禁用步骤如下：

在地址栏输入 `edge://net-internals/#hsts` 并访问

找到 **Delete domain security policies** 输入不想自动使用 HTTPS 的域名，并点击 **Delete**

Android 版的 Edge 浏览器也可以使用这个方法