+++
title = "Hugo をインストールする"
date = "2024-01-13T23:53:58+09:00"
toc = true
tags = ["hugo", "install"]
+++

Hugo をインストールします。

## 2種類の Hugo バイナリ

Hugo には標準版 (standard edition) と拡張版 (extended edition) の2種類があります。拡張版には次の機能が追加されています。

* 画像処理時に [WebP 形式](https://ja.wikipedia.org/wiki/WebP) にエンコードできる
* 組み込みの LibSass トランスパイラを使って [Sass を CSS にトランスパイルできる](https://gohugo.io/hugo-pipes/transpile-sass-to-css/)

どちらを選択すればよいか、よくわからないときは **拡張版 (extended edition)** のインストールをお奨めします。というのは、選択したテーマによっては Sass を使っていてビルドするときに拡張版を要求するときがあるからです。

## マルチプラットフォーム対応

Hugo はマルチプラットフォーム向けにインストール手段が提供されています。お使いのオペレーティングシステムにあわせて次のドキュメントを参照してインストールしてください。

* [Installation](https://gohugo.io/installation/)

多くの環境向けにツールのバイナリファイル (コマンド) が提供されているため、インストールはすぐに完了するでしょう。

インストールが完了したらターミナルでコマンドを実行してバージョンを表示してみましょう。

```bash
$ hugo version
hugo v0.121.2+extended linux/amd64 BuildDate=unknown
```

バージョンに `+extended` とついているのは拡張版をインストールしたからです。

## 高度な設定: Hugo をコンパイルインストール

> **前節でバイナリをインストールした方はこの作業を行う必要はありません**

プログラマーの方で自分のマシンに [Go 言語](https://go.dev/) のコンパイラをインストールしている方は最新バージョンをコンパイルしてインストールすることもできます。

* [Build from source](https://gohugo.io/installation/linux/#build-from-source)
  * Git, Go, GCC (または Clang) が必要

```bash
$ CGO_ENABLED=1 go install -tags extended github.com/gohugoio/hugo@latest
```

前節の実行例ではバージョン表記の `BuildDate=unknown` となっていたのは、私がローカルでビルドしたときにこの変数を設定していないからになります。
