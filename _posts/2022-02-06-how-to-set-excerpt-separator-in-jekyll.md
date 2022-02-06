---
layout: post
title: 如何在 Jekyll 文章中设置「阅读全文」？
date: 2022-02-06 22:06
category: Jekyll
tags: [jekyll]
summary: 
---

在首页显示文章的摘要内容，并提供跳转到全文页面的链接是一个常见的需求

在 Jekyll 中，将 `_config.yml` 中的 `excerpt_separator` 设置为欲使用的分隔符即可

在这个博客中，这行设置是 `excerpt_separator: <!-- more -->`

所以，在文章中输入 `<!-- more -->` 即可实现文章头部描述的需求

