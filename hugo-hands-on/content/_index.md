+++
title = "Hugo ハンズオン"
date = "2024-01-14T00:37:48+09:00"
+++

このハンズオンでは次の内容を学びます。

{{< ticks >}}
* [Hugo とは]({{< ref "post/what-is-hugo.md" >}})
* [Hugo のインストール]({{< ref "post/install-hugo" >}})
  * ハンズオンの前に必ずインストールしておいてください
* [Hugo のコンテンツビルド]({{< ref "post/build-content" >}})
  * このハンズオン資料そのものをビルドしてみましょう
* [Hugo のサイト構築とテーマ設定]({{< ref "post/new-site" >}})
  * [PaperMod](https://themes.gohugo.io/themes/hugo-papermod/) というテーマを使う
* [Hugo のコンテンツ作成]({{< ref "post/write-content" >}})
  * 記事を書きながらブラウザで内容をレビューする
{{< /ticks >}}

ハンズオンではここまでの内容を説明します。

---

ここから先は上級者向けに時間に余裕のある方が自分でやってみてください。

このハンズオン資料そのものが Hugo で作成されています。

リポジトリは [github.com/t2y/hugo-hands-on](https://github.com/t2y/hugo-hands-on) にあります。

先ほど使った PaperMod のテーマについては忘れてください。このハンズオン資料は [Cupper](https://themes.gohugo.io/themes/cupper-hugo-theme/) というテーマを使っています。必要に応じて次の情報も参考にしてください。

* [Cupper リポジトリ](https://github.com/zwbetz-gh/cupper-hugo-theme)
* [Cupper デモ画面](https://cupper-hugo-theme.netlify.app/)

実はこのハンズオン資料そのものがシンプルにみえて、少しテーマをカスタマイズしたり、テーマが提供する拡張機能を使っていたりします。

* Hugo のテーマを少しカスタマイズする
* Hugo の Shortcodes を使う

さらにリポジトリに修正内容を push すると自動的に [GitHub Pages](https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages) にデプロイしたりしています。GitHub Pages とは GitHub 社が提供する静的なサイトホスティングサービスです。GitHub のアカウントをもっていれば少し設定すれば無料で使えます。GitHub Pages というサービスを使って、このハンズオン資料はインターネット上に公開されています。

* Github Pages を使う
* GitHub Actions で Hugo の成果物をデプロイする
