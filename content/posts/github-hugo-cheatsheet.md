---
title: "GitHub Pages + Hugo ブログ：自分用チートシート"
date: 2026-09-14
draft: false
---

先生に教わりながらブログを作る過程で、自分用にまとめたメモです。

## 全体の流れ

```text
Markdownを書く
↓
HugoがHTMLに変換
↓
GitHub Actionsが自動実行
↓
GitHub Pagesで公開
```

## 主なファイルと役割

| ファイル | 役割 | ここを変えると… |
|---|---|---|
| `hugo.toml` | ブログ全体の設定 | ブログ名、URL、言語など |
| `layouts/index.html` | トップページ | ブログタイトル、説明文、Posts、記事一覧 |
| `layouts/_default/single.html` | 記事ページ | 記事タイトル、日付、本文の表示 |
| `static/css/style.css` | デザイン | フォント、文字サイズ、余白、色、スマホ表示 |
| `content/posts/○○.md` | 各記事 | タイトル、日付、本文 |
| `.github/workflows/hugo.yml` | 自動公開 | GitHub ActionsでHugoを動かす仕組み |

## 新しい記事を書くとき

新しい記事は、

```text
content/posts/new-post.md
```

のようなファイルを作ります。

中身は基本的にこうです。

```markdown
---
title: "記事タイトル"
date: 2026-09-14
draft: false
---

ここに本文を書きます。
```

## どこを直せばいい？

- ブログ名を変えたい  
  → `hugo.toml`

- トップページの説明文を変えたい  
  → `layouts/index.html`

- `Posts` や記事一覧の表示を変えたい  
  → `layouts/index.html`

- 記事ページの日付表示を変えたい  
  → `layouts/_default/single.html`

- フォント・文字サイズ・余白・色を変えたい  
  → `static/css/style.css`

- 新しい記事を書きたい  
  → `content/posts/`

- スマホ表示だけ調整したい  
  → `static/css/style.css` の `@media`

## 覚えておきたいこと

記事を書く場所と、見た目を変える場所は別です。

```text
記事を書く
↓
content/posts/

見た目を変える
↓
static/css/style.css
```

この2つを分けて考えると、かなり分かりやすくなります。

## スマホ表示

スマホで正しく表示するために、HTMLの `<head>` にはこれを入れておきます。

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

スマホ専用のCSSは、たとえばこう書けます。

```css
@media (max-width: 600px) {
  body {
    margin: 50px auto;
    padding: 0 20px;
    font-size: 18px;
  }
}
```

## 日付の考え方

記事ファイルには、

```markdown
date: 2026-09-14
```

のように保存しておきます。

表示するときは、Hugo側で好きな形に変えられます。

```html
{{ .Date.Format "January 2, 2006" }}
```

なら、

```text
September 14, 2026
```

のように表示されます。

---

始めたばかりですが、少しずつ自分のブログを育てていきます。
