---
title: "golang やってみた（その1）"
emoji: "💬"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["golang", "tutorial"]
published: true
---

## golang やってみた

### まずはインストール

色々端折っちゃいますが、golangをダウンロードしてきてインストーラを実行

### 最初のコマンド

```
mkdir hello
cd hello

go mod init example/hello
```

下記のような結果が返ってくる。

```
go: creating new go.mod: module example/hello
```

### hello.goファイルを作成する

```
touch hello.go
```

hello.goに下記を転記する。

```
package main

import "fmt"

func main() {
  fmt.Println("Hello, World!")
}
```

### 実行してみる

```
go run .
```

「Hello, World!」が出力された！

```
Hello, World!
```

### quoteパッケージを使ってみる

hello.goを下記に変更する。

```
package main

import "fmt"

import "rsc.io/quote"

func main() {
  fmt.Println(quote.Go())
}
```

この状態で`go run .`しても怒られる。
追加した`rsc.io/quote`をインストールしていないもんね。

```
go run .

hello.go:5:8: no required module provides package rsc.io/quote; to add it:
        go get rsc.io/quote
```

なので、下記を実行する。
このコマンドは、import対象のモジュールの過不足があればダウンロードや削除を行ってくれるらしい。

```
go mod tidy
```

```
go mod tidy
go: finding module for package rsc.io/quote
go: downloading rsc.io/quote v1.5.2
go: found rsc.io/quote in rsc.io/quote v1.5.2
go: downloading rsc.io/sampler v1.3.0
go: downloading golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c
```

これで実行できるか、と思いきや。。

```
go run .
```

```
Don't communicate by sharing memory, share memory by communicating.
```

ここまでで、Getting startedが終了。

### 参考リンク

* [Getting started](https://go.dev/doc/tutorial/getting-started)
* [実際にトライしたリポジトリ](https://github.com/it-walker/gorin/tree/master/hello)
