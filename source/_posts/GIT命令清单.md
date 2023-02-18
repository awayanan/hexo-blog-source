---
title: 优化工具
date: 2023-02-02 10:37:53
categories:
  - 技术笔记
tags: 
  - git
  - 开发工具
---
> 没有BUG的代码是不完整的

## 初始化代码库 init
通常由以下两种方式获取Git项目仓库的方式：
- 将尚未进行版本控制的本地目录转换为Git仓库
- 从其他服务器克隆一个已经存在的Git仓库
```commandline
git init                              # 在当前目录新建一个Git代码仓库
git init [project-folder]             # 新建目录,并将其初始化为一个Git代码库
git clone [url]                       # 克隆一个远端的完整仓库到当前目录下 
git clone [url] [destination-folder]  # 克隆一个远端的完整仓库到目标目录下
```
## 配置文件 config
首先要做的就是设置自己的名字和邮件地址
```commandline
git config --global user.name  "username"
git config --global user.email "example@example.com"
```
查看全局配置或者修改全局配置
```commandline
git config --list         # 显示Git配置文件
git config -e [--global]  # 编辑Git配置文件  
```
Git一般会自动着色大部分输出内容，如果喜欢朴素，也可以关掉。**没有RGB不干了**
```commandline
git config --global color.ui false
```
## 增加删除文件 add/rm

### 增加


### 删除

## 代码提交


### 本地仓库关联远端仓库

- 修改命令
  ```commandline
     git reset-url origin [url]
  ```
- 删除重新添加
  ```commandline
     git remote rm origin 
     git remote add origin [url]
  ```
