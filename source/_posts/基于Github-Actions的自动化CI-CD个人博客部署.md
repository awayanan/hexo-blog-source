---
title: 基于Github Actions的自动化CI/CD个人博客部署
date: 2023-01-24 01:37:53
tags: 
  - 技术笔记
  - hexo
toc: true
reward: false 
---
[toc]

# 你在干什么？

用hexo撰写博客很方便，还可以结合github action 自动化部署博客，心动不如行动。

那么，我想发布一个Github Pages，那我就需要开发一个项目可以部署Github Pages的项目，这个项目就相当于源代码项目，发布的Github Pages则作为部署项目即是保存的最终的网页文件。

简单来说，hexo-blog-source为源代码开发项目，yourname.github.io为网页文件部署项目。


# 准备开始干？
## 一些准备工作
- git
- node.js
- hexo
- 域名（个性化）
- ...
- 腊月天气

### 准备环境
1、`git`环境配置：略
- 环境测试
```
git -v
```

2、`node.js`环境安装：略
- 环境测试
```bash
node -v
npm -v
```

3、`github`密钥配置：略，详情见github官方文档：如何创建[个人访问令牌](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)。
- 如何应用，在设置中新建一个名为**ACCESS_TOKEN**的密钥，然后进入开发项目，在该项目的配置加入该个人密钥。

3、hexo环境配置
- 使用npm安装hexo博客程序
```bash
npm install -g hexo-cli --registry=https://registry.npm.taobao.org  # 安装淘宝源npm
npm install -g cnpm --registry=https://registry.npm.taobao.org  # 安装淘宝源cnpm
```
- 初始化组件及预览
```bash
hexo init
hexo clean
hexo g
hexo s
hexo d
```
- 其他问题，如出现**ERROR Deployer not found: git**，执行以下
```bash
npm uninstall hexo-deployer-git
npm install -- save hexo-deployer-git
hexo d
```

4、hexo组件的一些介绍





# 干不完了。。
