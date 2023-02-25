---
title: "golang やってみた（2）"
emoji: "✨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["golang", "tutorial"]
published: true
---

## Tutorial: Create a Go module

### 新しいフォルダを作成します

```
mkdir greetings
cd greetings
```

### 初期化

```
go mod init example.com/greetings
```

こんな結果が出力されたらOK。

```
go: creating new go.mod: module example.com/greetings
```

ちなみに`go mod init`コマンドはコードの依存関係を追跡するために、go.modというファイルを作成するんですって。

ここから、greetings.goというファイルを作成して中身を記述していきます。

```
touch greetings.go
```

```
package greetings

import "fmt"

// Hello returns a greeting for the named person.
func Hello(name string) {
  // Return a greeting that embeds the name in a message.
  message := fmt.Sprintf("Hi, %f. Welcome!", name)
  return message
}
```

### 作ったgreetingsパッケージをhelloから呼び出す

helloフォルダへ移動します。

```
cd ../hello
```

hello.goを下記に書き換える。

```
package main

import (
	"fmt"

	"example.com/greetings"
)

func main() {
	// Get a greeting message and print it.
	message := greetings.Hello("Gladys")
	fmt.Println(message)
}
```

下記コマンドを実行する。
このコマンドは、依存関係を見つける目的でexample.com/greetingを../greetingsに置き換えるよう指定する。

```
go mod edit -replace example.com/greetings=../greetings
```

```
go mod tidy
```

### 実行
出来上がったので下記を実行してみる。

```
go run .
```

できた！

```
Hi, Gladys. Welcome!
```
