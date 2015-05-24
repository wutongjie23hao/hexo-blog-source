title: git创建与合并分支
date: 2015-05-24 16:23:19
tags: git
categories: 技术
---
* 创建分支:``git checkout -b dev``
* 合并分支:
```git
git checkout master
git merge dev
```
* 转换分支:``git checkout dev``