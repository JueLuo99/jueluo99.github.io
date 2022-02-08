---
layout: post
title: 解决 Markdown 中表格内出现竖线“|”时无法正常渲染的问题
date: 2018-12-12 17:17
category: Markdown
tags: [markdown, html]
---

在 Markdown 中，表格内出现竖线“|”会被认为是表格的一部分

<!-- more -->

## 解决思路
- Markdown 最后是会被转换成 HTML 故使用 ```<code>``` 标签来解决
- ```|``` 在 HTML 中传输使用的 ACSII 码为 ```124```，故使用 ```&#124;``` 替换之

## 示例
|列1|列2|列3|
|---|---|---|
|debug|<code>debug [0&#124;1]</code>|切换 debug 模式的开关|

## 参考
1. [ASCII码对照表][1]
2. [How to escape a pipe char in a code statement in a markdown table? - Stack Overflow][2]


  [1]: http://tool.oschina.net/commons?type=4
  [2]: https://stackoverflow.com/questions/17319940/how-to-escape-a-pipe-char-in-a-code-statement-in-a-markdown-table/17320389#17320389