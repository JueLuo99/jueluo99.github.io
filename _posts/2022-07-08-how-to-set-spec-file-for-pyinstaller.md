---
layout: post
title: 调整 Pyinstaller 的 spec 文件来控制打包哪些内容
date: 2022-07-08 08:53
category: Python
tags: [python, pyinstaller]
---

案例：需要打包一个 Python 项目为二进制文件，但该项目包含了一个 `config.py` 不应一起被打包

## 安装 Pyinstaller


```bash
pip install pyinstaller
```

## 创建 spec 文件

使用如下命令获得一个 `.spec` 文件：

```bash
pyinstaller monitor.py
```

## 调整 spec 文件

在本例中，需要调整如下两行：

告知 Pyinstaller 将 `config.py` 置于打包后的根目录中
```spec
datas=[('config.py', '.')],
```

告知 Pyinstaller 不将 `import config` 一起打包
```spec
excludes=['config'],
```

## 打包，创建可执行文件

修改 `.spec` 后再执行：

```bash
pyinstaller monitor.spec
```