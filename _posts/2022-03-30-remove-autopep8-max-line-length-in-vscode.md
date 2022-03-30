---
layout: post
title: 移除 VScode 中 autopep8 的最大行长度限制
date: 2022-03-30 09:43
category: Python
tags: [python, vscode]
---

### 方法一

在 settings.json 中加入以下设置：
```json
"python.formatting.provider": "autopep8",
"python.formatting.autopep8Args": [
    "--max-line-length=200"
],
```

### 方法二

1. 按 <kbd>Ctrl</kbd> + <kbd>,</kbd> 打开设置
1. 搜索 ```python.formatting.autopep8Args```
1. 点击 <kbd>Add Item</kbd>
1. 写入 ```--max-line-length=200```

