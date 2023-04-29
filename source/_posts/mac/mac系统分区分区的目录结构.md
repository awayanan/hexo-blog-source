---
title: mac系统分区分区的目录结构
toc: true
copyright: true
reward: true
tags: mac
abbrlink: 21639fef
date: 2023-04-27 23:25:01
description:
---

>不同于windo ws的多根逻辑存储结构，os x是单根逻辑存储结构的，这是因为os x底层是unix系统，其目录结构是按照unix系统规范来的。
<!--more-->


| dir                        | description                                                       |
|:---------------------------|:------------------------------------------------------------------|
| /bin                       | 传统unix命令的存放目录，如ls，rm，mv等。                                         |
| /sbin                      | 传统unix管理类命令存放目录，如fdisk，ifconfig等等。                                |
| /usr                       | 第三方程序安装目录                                                         |
| /usr/bin                   | 动态链接库                                                             |
 | /usr/sbin                  | 动态链接库                                                             |
| /usr/lib                   | 动态链接库，该目录中存放了共享库                                                  |
| /etc.                      | 标准unix系统配置文件存放目录，如用户密码`/etc/passwd`。此目录实际为指向`/private/etc`的链接     |
| /dev                       | 设备文件存放目录，如何代表硬盘的`/dev/disk0`                                      |
| /tmp                       | 临时文件存放目录，权限为所有人任意读写。此目录实际为指向`/private/tmp`的链接                     |
| /var                       | 存放经常变化的文件，如日志文件。此目录实际为指向`/private/var`的链接                         |
| /Applications              | 应用程序目录，默认所有的`GUI`应用程序都安装在这里                                       |
| /Library                   | 系统的数据文件、帮助文件、文档等等                                                 |
| /Network                   | 网络节点存放目录                                                          |
| /System                    | 只包含一个名为`Library`的目录，这个子目录存放了系统的绝大部分组件，如各种`framework`，以及内核模块，字体文件等 |
| /Users                     | 存放用户的个人资料和配置。每个用户有自己的单独目录                                         |
| /Volumes                   | 文件系统挂载点存放目录                                                       |
| /cores                     | 内核转存储文件存放目录。当一个进程崩溃时，如果系统允许则会产生转储文件                               |
| /private                   | 里面的子目录存放了`/tmp`，`/var`，`/etc`等链接目录的目标目录                           | 
| /installer.failurerequests | 可能是用来记录发生crash时的日志                                                |
