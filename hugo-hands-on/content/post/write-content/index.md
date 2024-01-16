+++
title = "記事を書く"
date = 2024-01-17T00:05:13+09:00
toc = true
tags = ["hugo", "content"]
+++

[新規サイトの構築を完了]({{< ref "post/new-site" >}}) したら最初の記事を書いてみましょう。

## 記事を作成する前に

hugo のコマンドで記事を作成するときにメタデータの初期設定を管理するファイルがあります。

```
archetypes/default.md
```

デフォルトではドラフト機能が有効になっているため、このハンズオンではその設定を無効に設定します。`draft = false` に変更します。

```bash
+++
title = '{{ replace .File.ContentBaseName "-" " " | title }}'
date = {{ .Date }}
draft = false
+++
```

ドラフト機能とは下書き状態かどうかを管理し、下書きの記事を誤って公開しないようにするためのフラグです。このハンズオンでは重要ではないので無効にします。

> draft=true のときは開発サーバーや `hugo` コマンドで本番向けビルドしたときに出力されなくなります。その振る舞いも `hugo --buildDrafts` のようにオプションを指定することでドラフトの記事を出力するように変更できます。
> 
> [Draft, future, and expired content](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content)

## 記事のファイルを作成する

次のようにコマンドを実行してください。

```bash
$ hugo new posts/first-blog/index.md
Content "path/to/mysite/content/posts/first-blog/index.md" created
```

次の場所に `index.md` というファイルが作成されます。このファイルをテキストエディタで編集します。

```bash
$ ls content/posts/first-blog/
index.md
```

hugo の開発サーバーを起動している状態であれば、ファイルの作成と同時にホーム画面に **First Blog** というタイトルのカードのようなものが表示されます。

{{< figureCupper img="hugo-hands-on-write-content1.png" caption="ホーム画面" command="Resize" options="800x" >}}

そのリンクをクリックすると記事のページへ遷移します。

{{< figureCupper img="hugo-hands-on-write-content2.png" caption="記事のページ" command="Resize" options="800x" >}}

テキストエディタでここで作成した `index.md` ファイルを編集して保存してみましょう。

```
content/posts/first-blog/index.md
```

markdown 記法を使ってテキストがブラウザでどのように表示されるかを確認してみてください。また見出しは目次に反映されます。

* 見出しを作る
* 強調の太字を書く
* 箇条書きをする
* ハイパーリンクを表示する
* 引用を表示する
* 画像を表示する

{{< figureCupper img="hugo-hands-on-write-content3.png" caption="記事の編集" command="Resize" options="800x" >}}

書いては保存して、ブラウザで内容を確認して、また書いては保存して内容を確認する。この繰り返しで記事を書きます。

試行錯誤しながらやってみてください。

## 記事の編集を終えたら

実際の Web サーバーにデプロイするときは [本番環境向けのビルド]({{< ref "post/build-content#本番環境向けのビルド" >}}) を参照してください。
