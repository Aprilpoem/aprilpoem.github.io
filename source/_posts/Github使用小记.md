---
title: Github使用小记
date: 2018-10-18 10:09:10
tags: git
---

###Github使用小记
我的记性是真的不太好呀，记录一下常用的git命令

####git常用命令
- - -

`git add <file>`把文件修改提交到暂存区 (stage)
`git commit -m "info"`一次性把暂存区的所有内容提交到版本库里
每次commit相当于克隆工作区的文件并且记录修改，版本库里有历史版本的文件。
HEAD指针指向当前版本，`git reset --hard HEAD^`可以回退到上一个版本
- - -
**`git diff`用法：**
`git diff`    #是工作区(work dict)和暂存区(stage)的比较
`git diff --cached `   #是暂存区(stage)和分支(master)的比较
`git diff HEAD -- <file> `:打印出来的结果“+”代表工作区新增加的内容，“-”代表版本库新增加的内容

- - -
**关于撤销**
`git checkout -- <file>`撤销工作区的修改
`git reset HEAD <file>`如果已经add到暂存区，该指令是撤销暂存区里的修改，然后再执行checkout撤销工作区修改
- - -
**关于删除操作**
`git rm <file>`用于删除一个文件
- `rm <file>`删除了工作区的文件； `git checkout -- file`可以恢复
- `git rm <file>`删除了文件，而且把删除记录提交都了暂存区；先`git reset HEAD <file> 撤销暂存区里的删除修改`，然后再`git checkout -- file`恢复工作区文件
- 想要彻底删除文件，两步操作: 1`git rm` 2. `git commit`, 这时候就没法恢复删除的文件了，只能回退到版本库里的最新版本。

####远程仓库，github提供Git仓库托管服务
**本地库推送到远程库**

- `git remote add origin git@github.com:username/reponame.git`关联远程库
- `git push -u origin master `把本地库内容推送到远程库
>Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来, 之后只要'git push origin master'就能够更新远程库了(本地库先更新add和commit操作)。

**远程库克隆到本地**
- 进入文件夹，`git clone git@github.com:Aprilpoem/reponame.git`
这样本地文件夹中就出现了reponame的文件夹（git clone + 仓库地址）

**分支**

`git branch`查看已有分支
`git branch <name>`创建分支
`git checkout <name>`切换分支
`git checkout -b dev`:创建一个分支dev并且切换到该分支
`git merge <name>`合并某分支到当前分支
`git branch -d <name>`删除分支