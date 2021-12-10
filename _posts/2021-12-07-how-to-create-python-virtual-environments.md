---
layout: post
title: Python 创建虚拟环境的几种方法
date: 2021-12-07 03:01
category: Python
tags: [python, virtualenv]
---

本文简单记录、比较了自己使用过的几种 Python 虚拟环境工具，并提供了一些常用的命令

# 对比

下表中的内容仅保证在本文写作时（Python 3.10）的准确性，请自行检查内容是否过期

| 名称         | 内建标准库 | Python 版本隔离 |
| ------------ | ---------- | --------------- |
| `venv`       | ✔️          | ❌               |
| `virtualenv` | ❌          | ❌               |
| `conda`      | ❌          | ✔️               |
| `pyvenv`     | 已弃用     | -               |

还有其他同样优秀、功能各异的虚拟环境工具，本文未做详细介绍：
- [pyenv/pyenv: Simple Python version management](https://github.com/pyenv/pyenv)
- [pyenv/pyenv-virtualenv: a pyenv plugin to manage virtualenv (a.k.a. python-virtualenv)](https://github.com/pyenv/pyenv-virtualenv)
- [pyenv/pyenv-virtualenvwrapper: an alternative approach to manage virtualenvs from pyenv.](https://github.com/pyenv/pyenv-virtualenvwrapper)
- [virtualenvwrapper · PyPI](https://pypi.org/project/virtualenvwrapper/#history)
- [pipenv · PyPI](https://pypi.org/project/pipenv/)

# venv

## 安装

在 Python 3.3 及以后的版本中，`venv` 被包含在 Python 标准库中，不需要额外的安装步骤

## 创建

通常都创建在项目下的 `venv` 目录中（如果项目中有多个 Python 版本，可以创建多个 `venv` 目录）

Windows
```shell
> python -m venv venv
```

Linux
```bash
$ python3 -m venv venv
```

## 使用

Windows (cmd)
```shell
> .\venv\Scripts\activate.bat
```

Linux
```bash
$ source ./venv/bin/activate
```

## 退出

Windows (cmd)
```shell
> .\venv\Scripts\deactivate.bat
```

Linux
```bash
$ deactivate
```

## 删除

移除 `venv` 目录即可

# virtualenv

> `virtualenv` is a tool to create isolated Python environments. Since Python `3.3`, a subset of it has been integrated into the standard library under the venv module. The `venv` module does not offer all features of this library, to name just a few more prominent:
> - is slower (by not having the app-data seed method),
> - is not as extendable,
> - cannot create virtual environments for arbitrarily installed python versions (and automatically discover these),
> - is not upgrade-able via pip,
> - does not have as rich programmatic API (describe virtual environments without creating them).

操作方式与上文介绍的 `venv` 基本一致，但命令行工具名称不同

## 安装

```shell
pip install --user virtualenv
```

## 创建

```shell
virtualenv venv
```

这将创建一个与 `virtualenv` 版本相同的 python 虚拟环境到子目录 `venv` 中

## 使用、退出与删除

与上文的 `venv` 完全相同

# conda

## 安装

[Download Anaconda](https://www.anaconda.com/products/individual)

[Download Miniconda](https://docs.conda.io/en/latest/miniconda.html)

## 简单使用

| 功能                     | 命令                                               |
| ------------------------ | -------------------------------------------------- |
| 创建环境                 | `conda create --name $ENVIRONMENT_NAME`            |
| 创建指定版本的环境       | `conda create --name $ENVIRONMENT_NAME python=2.7` |
| 激活环境                 | `conda activate $ENVIRONMENT_NAME`                 |
| 退出环境                 | `conda deactivate`                                 |
| 安装一个包（激活环境后） | `conda install $PACKAGE_NAME`                      |
| 升级一个包（激活环境后） | `conda update $PACKAGE_NAME`                       |
| 卸载一个包（激活环境后） | `conda remove $PACKAGE_NAME`                       |
| 列出所有可用环境         | `conda env list`                                   |
| 删除一个环境             | `conda env remove --name $ENVIRONMENT_NAME`        |
|                          |

更多用法可参考官方文档：[Managing conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-conda.html)

# pyvenv

该模块[已在 Python 3.6 中被弃用](https://docs.python.org/dev/whatsnew/3.6.html#id8)

# 参考资料
1. [python - What is the difference between venv, pyvenv, pyenv, virtualenv, virtualenvwrapper, pipenv, etc? - Stack Overflow](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe/47559925)
1. [venv — Creation of virtual environments — Python 3.10.0 documentation](https://docs.python.org/3/library/venv.html)