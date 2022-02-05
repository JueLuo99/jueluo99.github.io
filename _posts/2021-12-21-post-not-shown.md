---
layout: post
title: 关于 Jekyll 编译通过但文章未显示的思考
date: 2021-12-21 17:56
category: Jekyll
tags: [jekyll]
---

昨日的文章 push 到 GitHub 后，打开 GitHub Pages 页面，发现新的文章并没有展示，故开始思考其未能正常展示的原因

首先想到的是，是不是 Jekyll 编译失败了？检查邮箱，未收到编译失败的提示邮件，检查 GitHub Actions 页面，也提示编译通过

然后检查了文件名和文件编码，文件名格式正确，编码也是 `UTF-8`，没有问题

最后通过翻阅 GitHub Actions 的 log，在 `build` 这个 job 的 `Build page with Jekyll` 中发现了这么一行内容：`Skipping: _posts/2021-12-20-python-flask-mysql.md has a future date`

这应该是由于时区不同导致的，但为何以前的 post 均没有出现该问题呢？