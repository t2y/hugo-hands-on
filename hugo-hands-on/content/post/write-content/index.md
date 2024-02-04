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

そのリンクをクリックすると記事のページへ遷移します。URL のパスもディレクトリの階層構造にある `first-blog` が含まれます。

{{< figureCupper img="hugo-hands-on-write-content2.png" caption="記事のページ" command="Resize" options="800x" >}}

作成した記事をブラウザで開いたら、テキストエディタからこの `index.md` ファイルを編集して、その都度、保存してみましょう。

```
content/posts/first-blog/index.md
```

例えば MarkDown 記法を使って記述したテキストがブラウザでどのように表示されるかを確認してみてください。また見出しのテキストは目次としても反映されます。

* 見出しを作る
* 強調の太字を書く
* 箇条書きをする
* ハイパーリンクを表示する
* 引用を表示する
* 画像を表示する

{{< figureCupper img="hugo-hands-on-write-content3.png" caption="記事の編集" command="Resize" options="800x" >}}

書いては保存して、ブラウザで内容を確認して、また書いては保存して内容を確認する。Hugo に限りませんが、静的サイトジェネレーターを使うときはこういった繰り返しで記事を書きます。

試行錯誤しながらやってみてください。

## 記事の編集を終えたら

実際の Web サーバーにデプロイするときは [本番環境向けのビルド]({{< ref "post/build-content#本番環境向けのビルド" >}}) を参照してください。

## (テキストだけの) 記事のファイルを作成する

基本的には前節で紹介したディレクトリを作成してその配下に `index.md` を作るやり方を覚えておけばよいです。このやり方だと、例えば記事の中に画像ファイルを表示したいときに `index.md` ファイルと同じディレクトリ内に画像ファイルを配置することで相対パスで画像ファイルを指定できて便利です。要は記事に使うメディアファイルも一緒にかためて整理できるのでわかりやすいというメリットがあります。

一方で別のやり方も紹介しておきます。画像ファイルなどはなく、ただテキストのみを管理したいという場合、わざわざディレクトリを作るのは面倒に感じるかもしれません。そういうときは次のようにコマンドを実行してください。

```bash
$ hugo new posts/ya-blog.md
Content "path/to/mysite/content/posts/ya-blog.md" created
```

content/posts 配下のディレクトリに直接 `ya-blog.md` というテキストファイルを配置して前節と同様の URL の命名規則 (`http://localhost:${ポート番号}/posts/ya-blog/`) でアクセスできることを確認してください。

{{< figureCupper img="hugo-hands-on-write-content5.png" caption="別の記事のページ" command="Resize" options="800x" >}}

content/posts 配下は次のようなディレクトリ構造は次のようになります。

```bash
$ tree content/posts/
content/posts/
├── first-blog
│   └── index.md
└── ya-blog.md

1 directory, 2 files
```
