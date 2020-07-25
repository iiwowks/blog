---
layout:        post
title:         "YAML 自定义功能"
date:          2020-07-05
category:      Markdown
author:        iiwowks
# comments:      false
published:     true
# photoswipe:    true
---

# simple sample

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

ページ設定：
- `title`: 标题
- `menutitle`: 出现在首页的副标题
- `cover: /assets/cover1.jpg` : ヘッダー画像
- `redirect_from: /PATH` : 変更元のPATHからこのページにリダイレクトする（可以用'- xxx'的数组形式）
- `comments: true` : Disqusによるコメント投稿を有効にする
- `published: false` : ページを非公開にする
- `latex: true` : 数式レンダリングを許可する
- `photoswipe: true` : 画像の拡大を有効にする
- `syntaxhighlight: false` : シンタックスハイライトを無効にしてページレンダリングを高速化する（特に数学、英語、雑文の記事での読み込み速度の高速化）
- `sitemap: false` : sitemap.xmlにリンクを追加しない (検索エンジンから少しだけ見つかりにくくなる)
- `feed: false` : feed.xmlにリンクを追加しない (RSSで更新情報を知らせない)
- `tags`:只在posts中使用
- `keywords`:只在pages中使用 
- `visible`:页面是否可见
- `weight`: 5 控制顺序
- `visible`: false 是否可见
- `language`:  en
- `permalink: "/about/" `: base_url/about/
> 参考文献：
[mako's blog](https://github.com/tex2e/blog)