---
title: Git命令清单
date: 2023-02-18 19:37:53
categories:
  - 技术笔记
tags: 
  - git
  - 开发工具
---
> 没有BUG的代码是不完整的

## 总览

![](/images/git.png)

## 初始化代码库

通常由以下两种方式获取Git项目仓库的方式：

- 将尚未进行版本控制的本地目录转换为Git仓库
- 从其他服务器克隆一个已经存在的Git仓库

```bash
git init                              # 在当前目录新建一个Git代码仓库
git init [project-folder]             # 新建目录,并将其初始化为一个Git代码库
git clone [url]                       # 克隆一个远端的完整仓库到当前目录下 
git clone [url] [destination-folder]  # 克隆一个远端的完整仓库到目标目录下
```

## 配置文件

首先要做的就是设置自己的名字和邮件地址

```bash
git config --global user.name  "username"
git config --global user.email "example@example.com"
```

查看全局配置或者修改全局配置

```bash
git config --list  # 显示Git配置文件
git config -edit   # 编辑Git配置文件  
```

Git一般会自动着色大部分输出内容，如果喜欢朴素，也可以关掉。**没有RGB不干了**

```bash
git config --global color.ui false
```

## 增加删除文件

工作目录下的每一个文件都不外乎是这两种状态：**已跟踪** 或 **未跟踪**。已跟踪的文件是指哪些被纳入了版本控制的文件，在上一次快照中是有它们的记录的，在工作一段时间后，它们的状态可能是未修改，已修改又或是已经放入暂存区。简单来说，已跟踪的文件就是Git已经知道的文件了。

当你初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪的文件，并且处于未修改状态，因为Git刚刚检出了它们，而你还没有对它们进行过编辑。

编辑过某些文件过，由于自上次提交后你对修改了它们，Git将它们标记为已修改文件。在工作时，你可以选择性地将这些修改过的文件放入暂存区，然后提交所有已暂存的修改，如此反复，而已。

### 增加

```bash
git add .                     # 添加当前目录的所有文件至暂存区
git add [dir]                 # 添加指定目录至暂存区
git add [file1] [file2] ...   # 添加指定文件至暂存区
```

如果对添加每个变化前，都想进一步确认，可以进行分次提交

```bash
git add -p
```

### 删除

```bash
git rm [file1] [file2] ...    # 删除工作区文件，并且将这次删除放入暂存区
git rm --cached [file]        # 停止追踪指定文件，但是文件会保留在工作区
git mv [file-from] [file-to]  # 更名文件，并将更名后的文件放至暂存区 
```

### 状态简览

```bash
git status         # 查看已被暂存的修改或未被暂存的修改
git status -s
git status --short
```

如果`git status`输出过于简略，不符合你想知道文件具体修改内容的需求，可以使用`git diff`命令。

```bash
git diff           # 比较工作目录中当前文件和暂存区快照之间的差异，或者是修改之后还没有暂存起来的变化内容
git diff --staged  # 比较已暂存文件与最后一次提交的文件差异
git diff --cached  # 查看已经暂存起来的变化
```

### 忽略文件

```bash
cat .gitignore
```

## 代码提交

```bash
git commit -m "msg"   			         # 提交暂存区文件至仓库区
git commit [file1] [file2] ... -m "msg"  # 提交暂存区的指定文件至仓库区
git commit -a                            # 提交工作区自上次commit之后的变化，直接提交至仓库区
git commit -v                            # 提交时显示所有的diff信息
```

### 撤销提交

在任何一个阶段中，你可能会想要撤销某些操作，

- 提交完后，发现漏了几个文件没有添加，或者提交信息写错了。怎么办？

```bash
git commit --amend  
```

只会将暂存区中的文件提交。如果自上次提交以来你还没有做出任何的修改，那么快照是会保持不变的，修改的只有提交信息。

```bash
git commit -m "first commit"
git add forgotten_file
git commit --amend -m [msg]         # 如果代码没有任何新的变化，则只是用来改写上一次的commit的提交信息
git commit --amend [file1] [file2]  # 重做上一次commit，并且包括指定文件的新变化
```

新建一个`commit`，用来撤销指定的`commit`

```bash
git revert [commit]
```

移除未提交的变化，稍后再移入

```bash
git stash
git stash pop
```

### 取消暂存的文件

比如说，你已经修改了两个文件并且想要将它们作为两次独立的修改提交，但是你不小心`git add *`全部暂存了这俩文件。如何取消俩暂存中的一个呢？

```bash
git reset HEAD [file] ...  # 取消暂存文件: 修改未暂存的状态
```

如果你也不想保留对文件的修改，怎么办？

```bash
git checkout -- [file]     # 撤销修改：该文件在本地的任何修改都会消失
```

### 恢复暂存区文件至工作区

```bash
git checkout [file]           # 恢复暂存区的指定文件至工作区
git checkout [commit] [file]  # 恢复某个commit的指定文件到暂存区和工作区
git checkout .                # 恢复暂存区所有文件至工作区
```

### 重置暂存区文件

```bash
git reset [file]           # 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
git reset --hard           # 重置暂存区和工作区，与上一次commit保持一致
git reset [commit]         # 重置当前分支的指针为指定commit，同时重置暂存区，但是工作区保持不变
git reset --hard [commit]  # 重置当前分支的HEAD为指定的commit，同时重置暂存区，但是工作区保持不变
git reset --keep [commit]  # 重置当前HEAD为指定的commit，但保持暂存区和工作区不变
```

### 查看提交历史

```bash
git log
git reflog                                 # 显示当前分支最近几次提交
git log -p[--patch] -2                     # 显示最近的两次提交差异
git log --stat                             # 显示每次提交的简略信息
git log --pretty=oneline  
git log --pretty=format:"%h - %an, %ar : %s"
git log --pretty=format:"%h %s" --graph    # 显示分支合并历史
```

```bash
git diff
git diff HEAD                         # 显示工作区与当前分支最新commit之间的差异
git diff --cached [file]              # 显示暂存区和上一次commit的差异
git diff --shortstat "@{0 day ago}"   # 显示今天写了多少代码
```

### 本地仓库关联远端仓库

- 修改命令

```bash
git reset-url origin [url]
```

- 删除重新添加

```bash
git remote rm origin     
git remote add origin [url]
```

## 远程仓库的使用

### 远程同步

```bash
git fetch [remote]        # 下载远程仓库的所有变动
git remote -v             # 显示所有远程仓库
git remote show [remote]  # 显示某个远程仓库的信息
```

### 关联远端

```bash
git remote add origin url  # 关联新的远程仓库,并命名
git push -u origin "main"  # 推送本地仓库至远程仓库
```

## 打标签


## 参考

[git-tips](https://github.com/yansheng836/git-tips)
