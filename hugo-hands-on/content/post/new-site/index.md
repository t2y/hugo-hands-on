+++
title = "新規サイトの構築"
date = 2024-01-14T14:21:23+09:00
toc = true
tags = ["hugo", "build", "theme"]
+++

ここでは一から自分のサイトを作ってみましょう。

## サイトの雛形を生成

`mysite` というディレクトリ配下にサイトに必要なファイル群を作成していきます。

```bash
$ hugo new site mysite
Congratulations! Your new Hugo site was created in path/to/mysite.

Just a few more steps...

1. Change the current directory to path/to/mysite.
2. Create or install a theme:
   - Create a new theme with the command "hugo new theme <THEMENAME>"
   - Install a theme from https://themes.gohugo.io/
3. Edit hugo.toml, setting the "theme" property to the theme name.
4. Create new content with the command "hugo new content <SECTIONNAME>/<FILENAME>.<FORMAT>".
5. Start the embedded web server with the command "hugo server --buildDrafts".

See documentation at https://gohugo.io/.
```

`mysite` ディレクトリの中身を確認します。

```bash
$ cd mysite/
$ ls
archetypes  assets  content  data  hugo.toml  i18n  layouts  static  themes
```

サイトを生成したときにテーマも選定して一緒にその設定をする必要があります。というのは、それぞれのテーマによって個別機能や拡張などがあるため、コンテンツの生成とテーマの設定は密接になっています。

## テーマの設定

ハンズオン資料と同じテーマを使うとおもしろくないので別のテーマを使ってみましょう。ここでは [PaperMod](https://themes.gohugo.io/themes/hugo-papermod/) というテーマを使って設定していきます。

> **テーマ選定のコツ**
> 
> [Hugo Themes](https://themes.gohugo.io/) ではたくさんの有志によるテーマが紹介されています。自分が作りたいスタイルにあうものを選択するとよいでしょう。一方でたくさんあり過ぎて、最初にどれを選択していいか迷うということもあるでしょう。テーマ選定に特別なやり方というものはありませんが、私は次のような手順でテーマを選択しています。
> 
> 1. ホーム画面の雰囲気から自分のイメージにあうものをいくつかピックアップする
> 1. ピックアップしたテーマのデモサイトを訪問する
>     * 例) [PaperMod のデモサイト](https://adityatelange.github.io/hugo-PaperMod/)
> 1. デモサイトでホーム画面の印象、コンテンツの導線、一覧とページの操作などを試してみる

(Hugo Themes を私が訪問したときの一番先頭に配置されていたテーマが PaperMod だったというのが本当の選定理由ですが) ここではいくつもテーマを見比べた結果 PaperMod を気に入ったと仮定して進めていきます。

テーマをクローンしてきます。これはそれぞれのテーマ紹介の画面からダウンロードすることもできますが、git コマンドを使った方が簡単なのでそうしています。テーマの紹介画面にはたいていインストール方法について説明されていると思います。PaperMod は [PaperMod のインストール](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation) にあります。テーマによってやり方が変わってくるのでそれぞれにあわせる必要があります。

```bash
$ git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1
```

正常にダウンロードできたらテーマのインストールそのものは完了です。

### hugo.toml の設定

テキストエディタで `hugo.toml` を編集します。次のように設定して保存してください。

```toml
baseURL = "https://example.org/"
languageCode = "ja-jp"
title = "My New Hugo Site"
theme = "PaperMod"
```

> **Hugo の設定ファイルのフォーマット**
> 
> Hugo ではデフォルトで [TOML](https://ja.wikipedia.org/wiki/TOML) というフォーマットを使います。[Configure Hugo](https://gohugo.io/getting-started/configuration/) を参照するとわかりますが、実は Hugo は toml, yaml, json の3つのフォーマットに対応しています。好みのマークアップ記法を用いて設定できます。これは一見、ユーザーの好みにあわせて自由度が高いようにみえますが、私はあまりよい仕様とは思えません。というのは、インターネットで Hugo の設定を調べたときに toml だったり yaml だったりで、同じ設定が異なるフォーマットでみつからからです。これは初心者を大いに混乱させます。例えば [PaperMod のデモサイトの設定サンプル](https://github.com/adityatelange/hugo-PaperMod/blob/exampleSite/config.yml) は yaml フォーマットで記述されています。[オンラインのフォーマット変換サービス](https://transform.tools/yaml-to-toml) などを使ってフォーマット変換して設定を参考にするとよいでしょう。
> 
> さらに Hugo の設定ファイルの名前はもともと `config.toml` だったのが、最近は `hugo.toml` に名前が変わったそうです。過去との互換性のために `config.toml` でも動作します。そして、これもオンラインで検索していると `config.toml` に行うと説明している設定もたくさん出てきます。

`hugo.toml` の設定を完了したら開発サーバーを起動してみましょう。`hugo.toml` が配置されているディレクトリで次のように実行します。停止するときは `Ctrl + C` を押下します。

```bash
$ hugo server
```

次のような、空っぽのホーム画面が表示されればテーマのインストールと初期設定は成功です。

{{< figureCupper img="hugo-hands-on-new-site1.png" caption="ホーム画面" command="Resize" options="800x" >}}

### テーマの詳細設定

ここまでの Hugo での作業はあまり難しくなかったのではないかと思います。しかし、Hugo で新規サイトを構築するときにもっとも難しい作業が実はテーマの詳細設定になります。というのは、テーマというのは見た目のカスタマイズだけでなく、ちょっとしたテンプレートのカスタマイズを実装していたり、外部ライブラリを使って機能拡張できるようにしているケースもあるからです。もちろん、そういった機能拡張は使わなければ設定しなくてもよいですが、そのテーマ独自の設定がたくさん出てきます。まだ使い始めたテーマのどの設定がどの機能に関連しているかなどわからないため、最初は試行錯誤しながら設定していくことになります。

テーマの紹介画面に簡単な設定についてのドキュメントはあるかもしれませんが、詳細な設定のドキュメントはないことが多いです。そんなときも役に立つのがデモ画面です。例えば [PaperMod のデモサイト](https://adityatelange.github.io/hugo-PaperMod/) があります。多くのテーマの開発者たちはデモサイトのソースコードや設定ファイルのソースをリポジトリで公開しています。どんな設定をすればよいかを [PaperMod のデモサイトのリポジトリ](https://github.com/adityatelange/hugo-PaperMod/tree/exampleSite) の設定ファイルをみて学ぶしかありません。

ここでは私があらかじめ確認して、ハンズオンで必要な設定のみを取り出した内容を紹介します。次の内容を `hugo.toml` にコピペしてください。実際のサイト構築では自分の気に入ったテーマに対して、こういった設定内容を自分で調べる必要があります。

```toml
baseURL = "https://example.org/"
languageCode = "ja-jp"
title = "Hugo のサンプルサイト"
theme = "PaperMod"
defaultContentLanguage = "ja"

[languages.ja]
languageName = "日本語"
weight = 1

  [languages.ja.taxonomies]
  category = "categories"
  tag = "tags"
  series = "series"

[[languages.ja.menu.main]]
name = "アーカイブ"
url = "archives"
weight = 5

[[languages.ja.menu.main]]
name = "検索"
url = "search/"
weight = 10

[[languages.ja.menu.main]]
name = "タグ"
url = "tags/"
weight = 10

[[languages.ja.menu.main]]
name = "WiKi"
url = "https://github.com/adityatelange/hugo-PaperMod/wiki/"

[params]
env = "production"
description = "PaperMod テーマを使ったサンプルサイト"
defaultTheme = "auto"
ShowShareButtons = true
ShowReadingTime = true
displayFullLangName = true
ShowPostNavLinks = true
ShowBreadCrumbs = true
ShowCodeCopyButtons = true
ShowRssButtonInSectionTermList = true
ShowAllPagesInArchive = true
ShowPageNums = true
ShowToc = true

  [params.homeInfoParams]
  Title = "サンプルサイトにようこそ"
  Content = """👋 Hugo ハンズオンの PaperMod をテーマに使ったサイトです。"""
```

一度 Hugo の開発サーバーのプロセスを `Ctrl + C` で停止してから再起動してみましょう。

```bash
$ hugo server
```

次のようなメニューと一緒にホーム画面が表示されれば成功です。

{{< figureCupper img="hugo-hands-on-new-site2.png" caption="テーマ設定を施したホーム画面" command="Resize" options="800x" >}}
