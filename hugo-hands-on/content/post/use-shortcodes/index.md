+++
title = "Hugo の Shortcodes を使う"
date = 2024-01-28T15:08:40+09:00
toc = true
tags = ["hugo", "template", "extension"]
+++

Hugo でコンテンツを書くときの拡張機能の1つであるショートコードについて紹介します。

## MarkDown 記法と表現の限界

Hugo では [MarkDown 記法のテキスト]({{< ref "post/sample-text" >}}) をビルドして HTML を生成することでブラウザで意図した表示になります。MarkDown 記法はプログラマーにとってのデファクト・スタンダードなマークアップ言語と言ってもよいぐらいに多くのところで使われています。最低限のテキストを書くのであれば MarkDown 記法で十分です。しかし、Web ページとしてリッチな表現を行いたいときに Markdown 記法にはその機能がありません。MarkDown テキストに生の HTML を記述することを Hugo は好ましく考えていません。

## ショートコードとは

Markdown 記法に足りない機能を補うために Hugo は [Shortcodes](https://gohugo.io/content-management/shortcodes/) という機能を提供しています。

ショートコードとは、具体的には Hugo のテンプレートを使った小さいスニペットです。例えば `youtube` の動画を表示するショートコードは次になります。その名前の通り、シンプルに記述できる短い特別な記法となっています。これは Markdown 記法ではありません。

> {{</* youtube id="Cc67K6O47XA" title="lofi beats Tokyo LosT Tracks -サクラチル- long mix" */>}}

{{< youtube id="Cc67K6O47XA" title="lofi beats Tokyo LosT Tracks -サクラチル- long mix" >}}

このショートコードは Hugo 自身が組み込みのショートコードとして提供しています。ソースコードは [hugo/tpl/tplimpl/embedded/templates/shortcodes/youtube.html](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/shortcodes/youtube.html) にあります。ブラウザに表示されたものとショートコードの実装を見比べることでなんとなく雰囲気はつかめると思います。

## Hugo の組み込みショートコード

一般的な用途の表現には Hugo が組み込みのショートコードとしてその機能を提供しています。[Use Hugo’s built-in shortcodes](https://gohugo.io/content-management/shortcodes/#use-hugos-built-in-shortcodes) でどのようなものがあるのかを確認してください。

画像を表示するには `figure` というショートコードを使います。

> {{</* figure src="https://gohugo.io/images/hugo-logo-wide.svg" caption="フーゴロゴ" width=240 */>}}

{{< figure src="https://gohugo.io/images/hugo-logo-wide.svg" caption="フーゴロゴ" width=240 >}}

X (旧Twitter) のポストを表示するには `tweet` というショートコードを使います。

> {{</* tweet user="GoHugoIO" id="917359331535966209" */>}}

{{< tweet user="GoHugoIO" id="917359331535966209" >}}

このように Markdown 記法では表現できないメディアファイルや外部サービスの埋め込みなどをコンテンツ内に簡潔に記述できます。

## サードパーティのショートコード

テーマによっては独自のショートコードを提供しているものもあります。例えば [Cupper](https://themes.gohugo.io/themes/cupper-hugo-theme/) では [Cupper Shortcodes](https://cupper-hugo-theme.netlify.app/cupper-shortcodes/) があります。Hugo 標準のショートコードよりもスタイルの一貫性があったり、ちょっとした拡張を提供していたりします。テーマを選択するときにどのようなショートコードがあるのかも調べてみるとよいでしょう。
