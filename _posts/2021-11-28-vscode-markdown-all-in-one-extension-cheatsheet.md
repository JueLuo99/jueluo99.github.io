---
layout: post
title: VS Code Markdown All in One 扩展快捷键备忘
date: 2021-11-28 01:54
category: 工具
tags: [markdown, vscode]
---

今日，[Typora](https://typora.io/) 推出了 `1.0.0` 正式版，并且变为了买断制收费软件，价格为 `$14.99 | 3 devices`，恰逢想把 Markdown 的写作整合进更常用的 VS Code 中，故开始寻找提升 Markdown 的写作体验的方法。

发现了一款名为 Markdown All in One 的插件，可以基本满足我的需求，在此简单记录下它在 Windows 下的快捷键

项目地址：https://github.com/yzhang-gh/vscode-markdown
商店地址：https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one

<!--more-->

## 自己对默认设置做出的一点调整

| 设置项                                        | 设置值  | 说明                                  |
| :-------------------------------------------- | :------ | :------------------------------------ |
| `markdown.extension.orderedList.autoRenumber` | `false` | 关闭自动编号有序列表项                |
| `markdown.extension.orderedList.marker`       | `one`   | 总是使用 `1.` 来标记有序列表项        |
| 快捷键中的 `markdown.extension.onTabKey`      | 移除    | 因为会覆盖掉 `Copilot` 等插件的快捷键 |

如此，即可愉快地使用以下功能啦

## 快捷键

| 功能           | 按键                                                                                |
| :------------- | :---------------------------------------------------------------------------------- |
| 切换粗体       | <kbd>Ctrl</kbd> + <kbd>B</kbd>                                                      |
| 切换斜体       | <kbd>Ctrl</kbd> + <kbd>I</kbd>                                                      |
| 切换删除线     | <kbd>Alt</kbd> + <kbd>S</kbd>                                                       |
| 提升标题等级   | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>]</kbd>                                   |
| 降低标题等级   | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>[</kbd>                                   |
| 切换数学环境   | <kbd>Ctrl</kbd> +  <kbd>M</kbd>                                                     |
| 切换任务项勾选 | <kbd>Alt</kbd> + <kbd>C</kbd>                                                       |
| 切换全屏预览   | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>V</kbd>                                   |
| 切换侧边预览   | <kbd>Ctrl</kbd> + <kbd>K</kbd> <kbd>V</kbd>                                         |
| 格式化表格     | <kbd>Alt</kbd> + <kbd>Shift</kbd> + <kbd>F</kbd>（与 VS Code 格式化代码快捷键相同） |

## 常用命令

默认按键 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> 后，输入命令

| 功能                                      | 命令                                                |
| ----------------------------------------- | --------------------------------------------------- |
| 创建目录                                  | Markdown All in One: Create Table of Contents       |
| 更新目录（通常会自动更新）                | Markdown All in One: Update Table of Contents       |
| 创建或更新章节编号[^1]                    | Markdown All in One: Add/Update section numbers     |
| 移除章节编号                              | Markdown All in One: Remove section numbers         |
| 切换行内代码块                            | Markdown All in One: Toggle code span               |
| 切换代码块                                | Markdown All in One: Toggle code block              |
| 打印当前文档成 HTML                       | Markdown All in One: Print current document to HTML |
| 打印多个文档成 HTML（会提示选择一个目录） | Markdown All in One: Print documents to HTML        |
| 切换数学环境（有快捷键）                  | Markdown All in One: Toggle math environment        |
| 将选中的文本切换为列表                    | Markdown All in One: Toggle list                    |

[^1]: 会自动按照多级标题等级编号，有一级标题的情况下，二级标题会被形如 `X.X. 这是标题` 样标记

## 其他功能

- 粘贴链接到选中的文本上，以将其直接转换为链接格式
- 图片地址、文件地址、数学公式的自动补全
