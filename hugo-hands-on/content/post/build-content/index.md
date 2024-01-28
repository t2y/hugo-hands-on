+++
title = "コンテンツをビルドする"
date = 2024-01-14T16:51:21+09:00
toc = true
tags = ["hugo", "build"]
+++

[Hugo のインストール]({{< ref "post/install-hugo.md" >}}) を完了したらこのハンズオン資料のリポジトリを使ってビルドしてみましょう。

## リポジトリのクローン

git コマンドを使って次のリポジトリをクローンします。

```bash
$ git clone https://github.com/t2y/hugo-hands-on.git ./repo
$ cd repo
$ git submodule update --init
```

リポジトリ配下の `hugo-hands-on` ディレクトリに移動します。

```bash
$ ls
LICENSE  README.md  hugo-hands-on
$ cd hugo-hands-on
$ ls
archetypes  content  hugo.toml  static  themes
```

## 開発サーバーの起動

hugo の開発サーバーを起動します。`hugo-hands-on` ディレクトリで実行するのに注意してください。

```bash
$ hugo server
port 1313 already in use, attempting to use an available port
Watching for changes in path/to/repo/hugo-hands-on/{archetypes,content,static,themes}
Watching for config changes in path/to/repo/hugo-hands-on/hugo.toml
Start building sites …
hugo v0.121.2+extended linux/amd64 BuildDate=unknown


                   | JA
-------------------+-----
  Pages            | 12
  Paginator pages  |  0
  Non-page files   |  0
  Static files     | 34
  Processed images |  0
  Aliases          |  0
  Sitemaps         |  1
  Cleaned          |  0

Built in 11 ms
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:45329/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

1313番ポートが空いているときはデフォルトで [http://localhost:1313](http://localhost:1313) で起動します。他に hugo の開発サーバーを起動している、または他アプリケーションがたまたまそのポート番号を使っているなど、使用済みのときはランダムにポート番号が設定されます。そのときは開発サーバーを再起動するごとにポート番号が変わるのでご注意ください。ブラウザで起動した開発サーバーのポート番号にアクセスするとこのハンズオン資料を確認できます。

{{< figureCupper img="hugo-hands-on-build1.png" caption="ホーム画面" command="Resize" options="800x" >}}

ここでホーム画面のコンテンツは `content/_index.md` ファイルになります。このファイルを編集して保存すると、その変更内容が即時で反映されることを確認してみましょう。

## 本番環境向けのビルド

開発サーバーでコンテンツをプレビューしながら編集して完成させます。その後、実際の Web サーバーには静的なコンテンツ (html/css/js と画像ファイルなど) を配置することになります。この作業を **デプロイ** と呼びます。デプロイする前に本番環境向けの静的なコンテンツを生成します。

```bash
$ hugo
Start building sites …
hugo v0.121.2+extended linux/amd64 BuildDate=unknown


                   | JA
-------------------+-----
  Pages            | 12
  Paginator pages  |  0
  Non-page files   |  0
  Static files     | 34
  Processed images |  0
  Aliases          |  0
  Sitemaps         |  1
  Cleaned          |  0

Total in 29 ms
```

`public` ディレクトリ配下にデプロイ用の静的なコンテンツが生成されます。

```bash
$ tree public/
public/
├── android-chrome-192x192.png
├── android-chrome-512x512.png
├── apple-touch-icon.png
├── browserconfig.xml
├── css
│   ├── fonts
│   │   ├── miriamlibre-bold.woff
│   │   └── miriamlibre-bold.woff2
│   ├── images
│   │   ├── arrow_effect.svg
│   │   ├── icon-tick.svg
│   │   └── stripe.svg
│   ├── myfavorite.css
│   ├── prism.css
│   ├── search.fe0cd54a21628574bff49d721c827d1bb165ab56b0f22dd55ae78addbe61c309.css
│   └── styles.css
├── favicon-16x16.png
├── favicon-32x32.png
├── favicon-96x96.png
├── favicon.ico
├── images
│   ├── browser-chrome-android.svg
│   ├── browser-chrome.svg
│   ├── browser-edge.svg
│   ├── browser-firefox-android.svg
│   ├── browser-firefox.svg
│   ├── browser-ie.svg
│   ├── browser-opera.svg
│   ├── browser-safari-ios.svg
│   ├── browser-safari.svg
│   ├── icon-info.svg
│   ├── icon-tag.svg
│   ├── icon-warning.svg
│   └── logo.svg
├── index.html
├── index.xml
├── install-hugo
│   └── index.html
├── js
│   ├── dom-scripts.js
│   ├── prism.js
│   ├── search.7aef046a0cc8b0c532f1d20087b920459bc868c936bb48a6ae221eceefca2d07.js
│   └── service-worker-registration.js
├── mstile-150x150.png
├── post
│   ├── index.html
│   └── index.xml
├── safari-pinned-tab.svg
├── site.webmanifest
├── sitemap.xml
├── tags
│   ├── hugo
│   │   ├── index.html
│   │   └── index.xml
│   ├── index.html
│   ├── index.xml
│   └── install
│       ├── index.html
│       └── index.xml
└── what-is-hugo
    └── index.html

11 directories, 50 files
```
