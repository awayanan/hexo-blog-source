---
title: Hexo新建标签、分类、归档、404等页面
toc: true
copyright: true
reward: true
tags:
  - hexo
categories:
  - 随笔
abbrlink: b81b42e4
date: 2023-04-27 23:55:11
description:
---


>基于标签、分类、归档
<!--more-->
👉hext主题的wiki[创建分类页面](https://github.com/iissnan/hexo-theme-next/wiki/%E5%88%9B%E5%BB%BA%E5%88%86%E7%B1%BB%E9%A1%B5%E9%9D%A2)

## 标签页面

1.新建一个页面，命名为 categories 。命令如下：
```shell
hexo new page "tags"
```

2.编辑刚新建的页面，将页面的类型设置为 categories ，主题将自动为这个页面显示所有分类。 进入目录/source/tages/index.md，设置其类型 type 值为“tages”
```commandline
---
title: tags
date: 2023-04-28 08:05:49
types: "tags"
---
```

3.进入目录 /themes/主题/_config.yml，把tages标签那项取消注释。如下所示：
```commandline
# Header-菜单
menu:
  归档: /
  标签: /tags
  笔记: /
  随笔: /
```

## 分类页面
[添加带统计的分类页面](https://yansheng836.github.io/article/521a17ae.html)

## 404页面

```commandline
hexo new page 404
```

## 主题优化

1.[取消页面广告fork-me](https://ligowi.github.io/2021/01/21/%E5%8E%BB%E6%8E%89fork-me-on-github-%E6%A0%87%E7%AD%BE/)


## 归档页面

[归档页面](https://blog.csdn.net/weixin_44330881/article/details/103315317)


## 代码复制功能
[添加复制代码块的功能](https://yansheng836.github.io/article/e9d1b881.html)
```python
print("hello world")
```

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```


## 代码块样式

1.代码高亮配置
安装hexo代码高亮插件 
```cnpm i -S hexo-prism-plugin```

修改`Hexo`根目录下`_config.yml`文件中`highlight.enable`的值为`false`，并新增`prism`插件相关的配置，主要配置如下：
```html
highlight:
  enable: false

prism_plugin:
  mode: 'preprocess'    # realtime/preprocess
  theme: 'tomorrow'
  line_number: false    # default false
  custom_css:
```

## 测试公式
`失败`
$x_{ij} \leq y_{ij}, \forall i \in I$