---
title: 基于Github Actions的自动化CI/CD个人博客部署
date: 2023-01-24 01:37:53
categories:
  - 技术笔记
tags: 
  - 博客
  - hexo
  - Github Actions
---
# 你在干什么？

用hexo撰写博客很方便，还可以结合github action 自动化部署博客，心动不如行动。

那么，我想发布一个Github Pages，那我就需要开发一个项目可以部署Github Pages的项目，这个项目就相当于源代码项目，发布的Github Pages则作为部署项目即是保存的最终的网页文件。

简单来说，hexo-blog-source为源代码开发项目，yourname.github.io为网页文件部署项目。

# 准备开始干？

## 一些准备工作

- git
- node.js
- hexo
- 域名（腾讯云、阿里云花几十块钱买一个，后续DNS解析一下）
- ...

### 准备环境

1、`git`环境配置：略

- 环境测试

```bash
git -v
```

2、`node.js`环境安装：略

- 环境测试

```bash
node -v
npm -v
```

3、`github`密钥配置：略，详情见github官方文档：如何创建[个人访问令牌](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)。

- 如何应用，在github中设置中新建一个名为**ACCESS_TOKEN**的密钥，然后进入开发项目，在该项目的配置加入该个人密钥。

4、hexo环境配置

- 使用npm安装hexo博客程序

```bash
npm install -g hexo-cli --registry=https://registry.npm.taobao.org  # 安装淘宝源npm
npm install -g cnpm --registry=https://registry.npm.taobao.org      # 安装淘宝源cnpm
```

- 初始化组件及预览

```bash
hexo init   # 初始化
hexo clean  # 清理缓存
hexo g      # 生成博客网页html
hexo s      # 本地预览
hexo d      # 推送

```

- 其他问题，如出现**ERROR Deployer not found: git**，执行以下

```bash
npm uninstall hexo-deployer-git
npm install -- save hexo-deployer-git
hexo d
```

- 执行`hexo s`进入本地访问地址预览博客

5、hexo博客组件简单介绍

```bash
├─_config.yml     # 博客的配置
├─public          # 生成的网页文件html
├─scaffolds       # 存放md默认模版的地方，后续每次新建md文件的默认模版如果要变动，修改post.md即可
├─source          # 存放博客源文件的地方，每次新建的md博客文件都会存放在这里
|   ├─_posts
|   |   ├─hello-world.md
|   |   ├─基于hexo的持续集成博客推荐.md
|   |   └我的第一篇博客.md
├─themes          # 博客的主题配置，网上挺多开源的，博主选用的是yilia-plus
```

具体来说，

- **_config.yml**
  网站的配置信息，可以在里面配置大部分的参数。

  修改_config.yml文件: theme: yilia-plus
- **package.json**
  应用程序的信息。有默认安装程序，可自行移除。
- **scaffolds**
  模版文件夹。新建文章时，hexo会根据scaffold来建立文件
  hexo的模版是指在新建文章中默认填充的内容。如，当我们修改scaffold/post.md中的Front-matter内容时，那么每次新建一篇文章时都会包含这个修改。
- **source**
  资源文件夹时存放用户资源的地方。
  _posts文件夹存放博客文档.md
- **themes**
  主题文件夹。hexo会根据主题来生成静态页面。

6、重点说一下 **_config.yml**

推送至自己的仓库，建一个名为yourgithubname.github.io的仓库，然后找到下面这里，修改推送的仓库，和要推送的分支

```yaml
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repo: git@github.com:yourname/yourname.github.io.git
  branch: main
```

到这里，一个基础的博客网页已经完成了，后续以下的步骤，每次自己新建文章然后重复部署推送的操作也是可以的。

```bash
hexo n "demo.md"
hexo g
hexo d
```

7、[hexo常用命令](https://hexo.io/docs/commands "hexo常用命令")

- **init**

```bash
hexo init [folder]  # 初始化网站，如果没有folder则会在当前目录下新建
```

- **new**

```bash
hexo new [layout] <title>  # 创建新文章。如果没有提供布局，Hexo 将使用 _config.yml 中的 default_layout。如果标题包含空格，请用引号将其括起来
```

- `-p`, `--path` 指定地址，自定义新建文章地址

```bash
hexo new page --path about/me "About me"  # 新建source/about/me.md
hexo new page --path about/me             # 新建source/_posts/about/me.md
```

- `-r`, `--replace` 如果文章存在则替换
- `-s`, `--slug` 自定义文章的`url`

截至此，所有的网页生成文件均在yourgithubname.github.io的仓库中，项目开发文件都在你当前所使用的电脑中，如果你要切换别的电脑的话就有些麻烦了，而且每次重复这些部署的命令也挺烦的。要是能每次推送完开发源代码，能自动给我部署就好了。

❤哎，这不就是CI/CD的路子嘛

# 干不完了。。

回到最初的起点，一个仓库只管推送源代码，另一个仓库存放自动生成的html文件。只需要关注推送的仓库，其他的一概不管，推送完自动部署即可。怎么实现。

## CI/CD（持续集成/持续部署）

### CI/CD概述

- CI: 指持续集成，属于开发人员的自动化流程。一次成功的CI表明应用代码的新更改会定期构建、测试并合并到共享存储库中。
- CD: 指持续交付或者持续部署。持续交付通常指开发人员对应用的更改会自动进行错误测试并上上传到存储库（如GitHub）,然后由运维团队将其部署到实时生产环境中。持续交付的目的也就是为了确保尽可能减少部署新代码时所需要的工作量。而持续部署指的是，自动将开发人员的更改从存储库发布到生产环境，以供客户使用。如下所示：

![](https://resources.github.com/assets/img/ci-cd/pipeline.png "CI-CD")

1. 在github上新建一个仓库，存放hexo源文件，如hexo-blog-source
2. 在该仓库配置**ACCESS_TOKEN**密钥
3. 在该仓库新建`main.yml`工作流，来生成并部署hexo网页，这个咋写后续再聊，很简单。

## 绑定域名

1. 花个几十去腾讯买个域名在yourname.github.io仓库目录下，新建`CNAME`，里面填上自己的域名，如`www.awayanan.wang`，由于这个仓库是由github actition工作流生成的，所以不要想着自己在仓库直接建，部署仓库下的文件皆由`main.yml`执行生成。
2. 域名绑定之后，要做dns解析，在哪家买的就直接用哪家的dns解析服务就行。

## 个性化页面

1. 404页面，个性化设置（后续）
2. 总结页面，个性化设置（后续）
3. 去除开源博客的广告，如果不知道在哪，打开网页检查，选中元素，即可知晓，本文选用的开源主题其广告是在页面右上角和页脚右侧，找到这两处的js文件，删除或者改成自己的链接即可。

## 评论功能

1. 直接开启Disqus最方便

## 页面刷新加速

1. 后续
