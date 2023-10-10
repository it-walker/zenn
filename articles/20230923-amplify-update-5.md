---
title: "@amplify/ui-reactを4.xから5.xにアップデートする"
emoji: "👋"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Update"]
published: true
---

## はじめに

Amplify を色々触っているうちに、どうやらボタンコンポーネントの新しいバリエーションが増えていることに気がつきました。
`@amplify/ui-react`のアップデートが必要みたいので、今回はアップデートを実践してみたいと思います。

## アップデートコマンド

もう、公式見ながらやってしまいますよ〜

```
npm install @aws-amplify/ui-react@5.x
```

```
npm install @aws-amplify/ui-react@5.x

removed 72 packages, changed 4 packages, and audited 2484 packages in 12s

263 packages are looking for funding
  run `npm fund` for details

6 high severity vulnerabilities

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
```

脆弱性の警告が出てるな。。あとで直さなきゃな。

## さっそく実装してみる

とりあえず横に並べてみましょう。
純粋に`@colorTheme`のみ書いた場合の例です。

```colorTheme.tsx
  <Flex gap="24px" margin="16px 16px">
    <Button colorTheme="info">
      info
    </Button>
    <Button colorTheme="overlay">
      overlay
    </Button>
    <Button colorTheme="success">
      success
    </Button>
    <Button colorTheme="error">
      error
    </Button>
    <Button colorTheme="warning">
      warning
    </Button>
  </Flex>
```

画面表示した結果がこちらです。

![](/images/20230923-amplify-update-5/2023-09-23-13-55-03.png)

## `@variant`と`@colorTheme`を組み合わせるとどうなるの？？

という疑問が湧いてきたので、やってみます。
結果、`destructive`、`warning`については`variant`が強く、それ以外は、`colorTheme`が有効になるんですね。

（一番上が、`variant`のみの表示。
2 つ目からは`variant`の設定をしつつ、`colorTheme`を設定してみた結果になります）

![](/images/20230923-amplify-update-5/2023-09-23-13-59-18.png)

## まとめ

というわけで、`@amplify/ui-react`を 4.x から 5.x アップデートをしてみたわけですが、特にトラブルなくアップデートできてしまいました。
`@colorTheme`と`@variant`の関係性については、基本的には`@colorTheme > @variant`の関係のようですが、`destructive`と`warning`については、`variant`が強く、指定しても影響しなそうです。

## 参考リンク

https://ui.docs.amplify.aws/react/getting-started/migration
