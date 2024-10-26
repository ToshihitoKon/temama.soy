---
title: いよいよちゃんとhugoでブログを作ろうと思った
date: 2024-10-12
slug: rebuild-blog-using-hugo
kind: page
draft: false
---

ずっと放置していた[temama.soy](https://temama.soy)をいい加減人に見せられるブログにしようと思って、ついに書き直しました。

主に

- 経歴(About)
- 作ってきたOSSの説明とかアップデートの記事(Tools)
- 雑記(Blogs)

を雑に残していくようにしたいところ。

## 構成

なにかをきっかけに知った[hugo](https://gohugo.io/)で作ってみることに  
更新頻度なんてたかが知れているので、プリレンダ(SSGって呼ぶらしい)のCMS探してたときに引っかかった記憶があります。

### テーマ選定 

[Hugo Themes](https://themes.gohugo.io/)のBlogタグをバーっと眺めて、気になったのは以下の4つ

- [adityatelange/hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod) ([demo](https://adityatelange.github.io/hugo-PaperMod/))
    - シンプル、動きが少ない
    - トップページのテキスト指定がconfigで書く前提がちょっと合わなかった
- [humrochagf/colordrop](https://github.com/humrochagf/colordrop) ([demo](https://humberto.io/))
    - 指定したテーマカラーが全体に配色されて印象がつく
    - 自分のテーマカラーは[中紅梅色](https://irocore.com/kobai-iro/)と決めているので印象づけに良さそうだった
- [Fastbyte01/KeepIt](https://github.com/Fastbyte01/KeepIt) ([demo](https://suspicious-archimedes-ab369d.netlify.app/))
    - シンプルなブログ向け 
- [g1eny0ung/hugo-theme-dream](https://github.com/g1eny0ung/hugo-theme-dream) ([demo](https://g1en.site/))
    - エントリ一覧に画像が並ぶと見やすくて良い
    - アイコンおしてポートフォリオ画面になるときのモーションがちょっと合わない

いくつか実際に触ってみて、1番目のPaperModを採用しました。理由としては

- 実際に記事をいくつか書いて配置してみて、考えていた通りの配置ができた
    - hugoのテーマは結構モノによってクセがあって一覧の出し方も違うので、デザインだけで選べなかった
- ポートフォリオよりブログとしての運用をメインにするので、トップページにブログ記事一覧を出せる
    - 途中一覧に並ぶのがBlogsかToolsのどちらかだけという問題が出たが、[ドキュメントにちっちゃく書いてあった](https://github.com/adityatelange/hugo-PaperMod/wiki/FAQs#posts-from-only-one-foldersection-visible-on-home-pag://github.com/adityatelange/hugo-PaperMod/wiki/FAQs#posts-from-only-one-foldersection-visible-on-home-page)
    - `params.mainSections`を指定しないとhugoのsites.mainSectionの探索を利用してしまい一部しか表示されないらしい

### デプロイ

GCE上にnginxを立ててそのまま`hugo`で生成したものをポン  
近々GitHub Actionsでデプロイできるようにするぞ（意気込み）

### 日英対応

日本語で書いた記事をChatGPTにぶち込んで英語記事を置いておく。  
読み直してニュアンス違いそうな場所は直しておこう、程度  
`記事名.ja.md`と`記事名.en.md`を置いておくだけでPaperModはリンクを置いておいてくれる。

---

hugoはいいですね、いずれ自分でもテーマを書いてみたいところ。  
どこかに中紅梅色を入れたい。
