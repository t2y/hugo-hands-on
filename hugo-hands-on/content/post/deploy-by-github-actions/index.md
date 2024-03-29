+++
title = "GitHub Actions で Hugo の成果物をデプロイする"
date = 2024-02-05T00:48:47+09:00
toc = true
tags = ["hugo", "github", "deploy", "build"]
+++

このハンズオン資料は [GitHub Pages](https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages) 上で公開されています。そして、リポジトリに変更を push すると、Hugo のコンテンツをビルドして自動的に GitHub Pages にデプロイします。

その自動デプロイを行っているのが [GitHub Actions](https://docs.github.com/ja/actions) になります。

## Hugo をデプロイするためのカスタムアクション

リポジトリの `.github/workflows/` 配下に GitHub Actions のワークフローファイルを作成します。そのワークフローファイルに Hugo のインストール、ビルド、GitHub Pages へのデプロイを自分で実装することもできますが、すでにサードパーティのカスタムアクションがあるのでそれを使った方が簡単でよいでしょう。

次の2つのカスタムアクションを使います。基本的にはリポジトリの README を参照してワークフローファイルを設定すればよいです。

* [peaceiris/actions-hugo](https://github.com/peaceiris/actions-hugo)
  * ジョブ環境に Hugo をインストールするためのカスタムアクション
* [peaceiris/actions-gh-pages](https://github.com/peaceiris/actions-gh-pages)
  * Hugo の成果物を `gh-pages` ブランチに push するためのカスタムアクション

このハンズオン資料のワークフローファイルは [.github/workflows/gh-pages.yml](https://github.com/t2y/hugo-hands-on/blob/main/.github/workflows/gh-pages.yml) になります。このファイルを参考にしながら設定してみてください。やっていることは次の4つです。

1. hugo-hands-on リポジトリをクローンする
1. 指定したバージョンの Hugo をインストールする
1. インストールした Hugo でリポジトリのコンテンツを [本番環境向けにビルド]({{< ref "post/build-content#本番環境向けのビルド" >}}) する
1. ビルドした成果物を `gh-pages` ブランチに push する (GitHub Pages へのデプロイをトリガー)

GitHub Actions の設定が正しいかどうかは実際に実行してみないとわかりません。設定に慣れないうちはエラーになることが多いでしょう。諦めずに何度もトライ&エラーを繰り返して設定しましょう。一度設定したら、そうそう変更することはなく、その後は自動デプロイしてくれるのでコンテンツの編集と公開を同期できます。

## gh-pages ブランチの作成

GitHub Pages へデプロイするためのブランチを `gh-pages` という名前で作ります。いまは任意のブランチ名で作ることもできますが、ひとまずこの名前で作ります。クリーンな gh-pages ブランチを作る方法が次の gist で紹介されています。同じようにやってみてください。

{{< gist ramnathv 2227408 >}}

## ワークフローに書き込み権限を与える

デプロイのための GitHub Actions のワークフロー内では `gh-pages` ブランチへ push します。ジョブ環境から書き込みできるようにするにはワークフロー内で使われるトークンに書き込み権限を与える必要があります。いくつか方法があります。

### リポジトリの設定画面から権限を与える

1つは GitHub のリポジトリの設定画面 (`settings/actions` の `General` ページ) から Workflow permissions という設定を探して *Read and write permissions* という項目を選択して設定を保存します。

{{< figure src="hugo-hands-on-deploy1.png" >}}

### ワークフローファイルに権限を記述する

もう1つはワークフローファイル (このハンズオン資料では [.github/workflows/gh-pages.yml](https://github.com/t2y/hugo-hands-on/blob/main/.github/workflows/gh-pages.yml) のこと) に直接、権限の設定を追加してしまう方法もあります。上述した設定画面のそれは次のように設定するのと同じです。

```yml
permissions:
  contents: write
```

## よくあるトラブルシューティング

GitHub Actions の設定に不備があるとスクリプト実行でエラーになったりします。ここでは筆者が経験したエラーを紹介します。

### gh-pages ブランチが存在しないときのエラー

GitHub Actions を実行して、Hugo のコンテンツビルドが成功して、その成果物を `gh-pages` ブランチに push しようとすると、次のような権限エラーが発生します。

```
/usr/bin/git push origin gh-pages
remote: Permission to t2y/hugo-hands-on.git denied to github-actions[bot].
fatal: unable to access 'https://github.com/t2y/hugo-hands-on.git/': The requested URL returned error: 403
Error: Action failed with "The process '/usr/bin/git' failed with exit code 128"
```
