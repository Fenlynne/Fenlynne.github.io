---
title: Git学习笔记
date: 2019-08-15 14:33:29
tags:
---
这是我的第一个git笔记.虽然以前零零散散学过几次git但都没有系统地整理过,这次把它记录下来免得以后再重学.

## 基础

### 初始配置

```console
$ git init
$ git config --global user.name = "name"
$ git config --global user.email = "email"
```

### 提交本地代码

```console
$ git add [filename]
$ git commit -m "your comment"

$ git add .
.gitignore文件可以用于排除
```

### 查看改动

查看当前未提交的改动过的文件

```console
$ git status 
```

查看具体改动

```console
$ git diff
```

### 查看提交记录

```console
git log
```

### 撤销未提交的更改

```console
$ git checkout [filename]
```

### 版本回退

```console
$ git reset --hard [版本号] 
```

查看历史

```console
$ git reflog
```

### 关联github

```console
$ git remote origin master "repo_adress"

```
### 推送到github
```
$ git push origin [branch_name]
```
## 分支管理

### 创建分支

```console
$ git branch branch_name
```

### 切换分支

```console
$ git checkout [-b]  branch_name
或者
$ git switch [-c]  branch_name
```

参数表示创建并切换

### 查看分支

```console
$ git branch
```

### 合并分支

```console
合并指定分支到当前分支
$ git merge branch_name
```

### 删除分支

```console
$ git branch -d branch_name
```
