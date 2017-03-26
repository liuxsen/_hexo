---
title: hexo
date: 2017-03-02 21:59:16
tags: hexo
---

> hexo next 主题中的404问题

**tags**

{% asset_img tags.png %}

**about**

{% asset_img about.png %}

新建一个 `about` 页面：

```
hexo new page "about"
```

菜单显示 `about` 链接，在主题的 `_configy.yml` 设置中将 `menu` 中 `about` 前面的注释去掉即可。

```
menu:
  home: /
  archives: /archives
  tags: /tags
  about: /about
```


添加一个 分类 页面，并在菜单中显示页面链接。

1. 新建一个页面，命名为 `categories` 。命令如下：

        hexo new page categories

1. 编辑刚新建的页面，将页面的类型设置为 `categories` ，主题将自动为这个页面显示所有分类。

        title: 分类
        date: 2014-12-22 12:39:04
        type: "categories"
        ---

    注意：如果有启用多说 或者 Disqus 评论，默认页面也会带有评论。需要关闭的话，请添加字段 `comments` 并将值设置为 `false`，如：

        title: 分类
        date: 2014-12-22 12:39:04
        type: "categories"
        comments: false
        ---

1. 在菜单中添加链接。编辑主题的 `_config.yml` ，将 `menu` 中的 `categories: /categories` 注释去掉，如下:

        menu:
          home: /
          categories: /categories
          archives: /archives
          tags: /tags
