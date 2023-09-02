---
title: "Amplifyのテーマ設定にはまる"
emoji: "📘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Theming", "React"]
published: true
---

## Amplifyのテーマ設定について学ぶ（はずだった）

今回は、`Amplifyのテーマ設定について`学びを得たかったのですが、実装はうまくできるものの、テストで怒られるという事象が発生してしまったので、そのことについて書こうと思います。

## Theme設定

`Amplify UI`の[ドキュメント資料](https://ui.docs.amplify.aws/react/getting-started/usage)のまんまですが、下記のように記載すると、テーマの設定を変更することができます。

```
import '@aws-amplify/ui-react/styles.css' // <--ここにデフォルトのテーマ設定がある

// テーマ設定
const theme = {
  name: 'custom-button-theme',
  tokens: {
    components: {
      button: {
        // this will affect the font weight of all Buttons
        fontWeight: { value: '{fontWeights.black.value}' },
        // this will only style Buttons which are the "primary" variation
        primary: {
          backgroundColor: { value: 'rebeccapurple' },
          _hover: {
            backgroundColor: { value: 'hotpink' },
          },
        },
      },
    },
  },
}

function App() {
  return (
    <ThemeProvider theme={theme}>
      <Button
        variation="primary"
      >
        Add to Cart
      </Button>
    </ThemeProvider>
  )
}
```

通常時：

![](/images/amplify-react-theming/2023-09-02-13-55-08.png)

ボタンカーソルホバー時：

![](/images/amplify-react-theming/2023-09-02-13-55-37.png)

バージョンの一覧を上げておこう。。

```
  "dependencies": {
    "@aws-amplify/ui-react": "^5.3.0",
    "@testing-library/jest-dom": "^5.17.0",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "@types/jest": "^27.5.2",
    "@types/node": "^16.18.46",
    "@types/react": "^18.2.21",
    "@types/react-dom": "^18.2.7",
    "aws-amplify": "^5.3.10",
    "aws-amplify-react": "^5.1.43",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1",
    "typescript": "^4.9.5",
    "web-vitals": "^2.1.4"
  },
```

というわけで、`import '@aws-amplify/ui-react/styles.css'`でデフォルトのテーマ設定を呼び出して、
`const theme = ...`で差分の設定を上書きすることで、テーマの設定を変更することができるようです。

と、ここまでは良かったのですが、テストの実行時になぜか下記のエラーが発生してしまいます。

```
Cannot find module '@aws-amplify/ui-react/styles.css' from 'src/App.tsx'
```

![](/images/amplify-react-theming/2023-09-02-14-05-29.png)

実行はうまくいくのになんでだろう・・・。

とりあえず、原因がわからないなりにジタバタしてみたいと思います。
あるあるですが、`node_modules`フォルダを削除して、パッケージを再インストールしてみます。

が、結果変わらずでした。。

とりあえず、実装が動かないわけじゃないのと、テスト実行のみ発生しているのでひとまず寝かせておこうかと思います。
また原因がわかったら共有していきたいと思います。
