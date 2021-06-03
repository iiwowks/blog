---
layout: post
title: "yaml页面设置"
date: 2020-08-17
category: Others
author: zhengjunan
published: true
latex: true
---

# simple sample

在没有特殊的配置情况下，必须添加的页面`yaml frontmatter`

```
---
layout:        post
title:         "YAML 自定义功能"
date:          2020-07-05
category:      markdown
author:        iiwowks
published:     true
---
```

| 属性                        |                说明                 |          默认值           |
| :-------------------------- | :---------------------------------: | :-----------------------: |
| `title`                     |                标题                 |                           |
| `menutitle`:                |         出现在首页的副标题          |                           |
| `cover: /assets/cover1.jpg` |              页眉图片               | 在`_data/autor.yml`中修改 |
| `redirect_from: /PATH`      |               重定向                |                           |
| `published: false`          |            是否发布页面             |                           |
| `latex: false`              |              公式渲染               |         **false**         |
| `photoswipe: true`          |            图像放大功能             |         **false**         |
| `syntaxhighlight: true`     |           代码块语法高亮            |         **true**          |
| `tags`                      |          只在 posts 中使用          |                           |
| `keywords`                  |          只在 pages 中使用          |                           |
| `weight`: 5                 |            控制页面顺序             |                           |
| `visible`: false            |              是否可见               |                           |
| `language`: en              |              页面语言               |                           |
| `permalink: "/about/" `     | 设置页面的链接: **base_url/about/** |                           |
| `feed: false`               |                删了                 |                           |
| `sitemap: false`            |                删了                 |                           |
| `comments: true`            |                删了                 |                           |

> 参考文章：

1. [mako's blog](https://github.com/tex2e/blog)
2. [博客主题](https://github.com/jwillmer/jekyllDecent)
