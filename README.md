# hugo-hands-on

Hugo ハンズオンチュートリアル

## リポジトリのクローン

themes を git submodule で管理しているため、リポジトリをクローンしたときにそのリポジトリを取得する必要がある。

```bash
$ git clone git@github.com:t2y/hugo-hands-on.git
$ git submodule update --init
```

## 記事の作成方法

```bash
$ cd hugo-hands-on/
$ hugo new post/install-hugo.md
Content "path/to/hugo-hands-on/content/post/install-hugo.md" created
```

ホームメニューのコンテンツは特別に `_index.md` というファイル名で content 直下に作成する。

```bash
$ hugo new _index.md
Content "path/to/hugo-hands-on/content/_index.md" created
```
