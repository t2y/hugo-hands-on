+++
title = "Hugo のテーマをカスタマイズする"
date = 2024-01-28T15:05:58+09:00
toc = true
tags = ["hugo", "theme"]
+++

このハンズオン資料は [Cupper](https://themes.gohugo.io/themes/cupper-hugo-theme/) というテーマを使っています。

## テーマのディレクトリ構成

このテーマのインストールは次のように cupper-hugo-theme というリポジトリをそのまま `themes/` 配下に配置しています。

```bash
$ git submodule add https://github.com/zwbetz-gh/cupper-hugo-theme.git themes/cupper-hugo-theme
$ git submodule update
```

ディレクトリ階層は次のようになります。

```bash
$ tree -L 2 themes/
themes/
└── cupper-hugo-theme
    ├── LICENSE
    ├── README.md
    ├── archetypes
    ├── assets
    ├── data
    ├── exampleSite
    ├── i18n
    ├── images
    ├── layouts
    ├── local_git_config.sh
    ├── netlify.toml
    ├── static
    ├── task_regen_toc.sh
    ├── task_serve.sh
    └── theme.toml

9 directories, 7 files
```

この階層の配下にテーマのソースコードがすべてあると考えてください。

[Custom CSS and JS](https://themes.gohugo.io/themes/cupper-hugo-theme/#custom-css-and-js) からカスタマイズした CSS の配置場所と設定についてドキュメントがあります。もしくは次のサンプルの設定ファイルをみた方がイメージしやすいかもしれません (オリジナルの yaml を toml に変換) 。

```yaml
[params]
...
customCss = ["css/custom_01.css", "css/custom_02.css"]
```

`hugo.toml` に次のような設定を追加し、この `myfavorite.css` という設定は `static/css/myfavorite.css` に配置します。[Directories](https://gohugo.io/getting-started/directory-structure/#directories) では `static` ディレクトリはサイト構築時に公開ディレクトリにコピーされるファイルを含む場所であることが説明されています。Hugo では外部からアクセス可能な任意のファイルは置く場所になります。

```toml
customCss = ["css/myfavorite.css"]
```

## テーマの CSS のデバッグ

ここで Cupper のデフォルトの行間サイズをカスタマイズしたいとします。行間のサイズを扱う CSS のプロパティは [line-height](https://developer.mozilla.org/ja/docs/Web/CSS/line-height) です。Google Chrome デベロッパーツールを使ったり、`themes/` 配下のコードを検索したりしてどこで定義されているのかを調べていきます。どうやって CSS の定義を調べるかというのを文章で説明するのは難しいのですが、試行錯誤しながらやっていくしかない気がします。

```bash
$ grep -ri line-height themes/*
themes/cupper-hugo-theme/static/css/prism.css:	line-height: 1.5;
themes/cupper-hugo-theme/assets/css/search.css:  line-height: 1.6;
themes/cupper-hugo-theme/assets/css/template-styles.css:    line-height: 1.5;
themes/cupper-hugo-theme/assets/css/template-styles.css:    line-height: 1.125;
themes/cupper-hugo-theme/assets/css/template-styles.css:    line-height: 1;
themes/cupper-hugo-theme/assets/css/template-styles.css:    line-height: 1.25;
themes/cupper-hugo-theme/assets/css/template-styles.css:    line-height: 1.125;
themes/cupper-hugo-theme/assets/css/template-styles.css:    line-height: 1.6;
themes/cupper-hugo-theme/assets/css/template-styles.css:    line-height: 1.25;
themes/cupper-hugo-theme/assets/css/template-styles.css:    line-height: 1;
themes/cupper-hugo-theme/assets/css/template-styles.css:    line-height: 1;
```

{{< figureCupper img="hugo-hands-on-html-line-height1.png" caption="Google Chrome デベロッパーツールのスタイル画面" command="Resize" options="400x" >}}

`html` という要素に line-height というプロパティが設定されていることがわかります。theme のソースコードを検索すると `themes/cupper-hugo-theme/assets/css/template-styles.css` に次のような設定をみつけられます。

```css
html {
    font-size: calc(1em + 0.33vw);
    font-family: Arial, Helvetica Neue, sans-serif;
    line-height: 1.5;
    color: #111;
    background-color: #fefefe;
}
```

## カスタム CSS の定義

ここで変更したいのは line-height のみです。このようなときは次のように変更したプロパティのみを記述します。

* `static/css/myfavorite.css`

```css
html {
    line-height: 1.75;
}
```

これだけで line-height の値をカスタマイズできます。数字を変更してみて、ブラウザ表示される行間が実際に更新されるかを試してみましょう。うまく更新されないときは Hugo の開発サーバーを再起動してください。
