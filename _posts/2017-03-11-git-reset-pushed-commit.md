---
layout: post
title: Git 撤销已经 push 到远端的 commit
date: 2017-03-11 22:36
category: Git
tags: [git, github, gitee]
---

本文适用于强迫症想保持 commits 记录整洁，但不小心提交了不必要内容的情况

## 情况一：本地不需要回退（即让远端回退到本地的版本）
  - 提交到远端
```
git push origin <分支名> --force
```

## 情况二：本地需要回退
 - 先在本地回退到需要的版本
```
git reset --hard <需要回退到的版本号（只需输入前几位）>
```
版本号可用如下指令查看
```
git log remotes/origin/分支名
```
 - 提交到远端
```
git push origin <分支名> --force
```