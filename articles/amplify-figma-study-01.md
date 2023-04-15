---
title: "ボタンコンポーネントをfigmaで作成してAmplifyに取り込んでみた"
emoji: "🐥"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["amplify", "figma"]
published: true
---

## 概要
最近Amplifyの沼にどっぷり使っています。
デザインをfigmaでやっているのですが、これがなかなか思った通りに動いてくれない・・
少しずつ知見を貯めていこうということで、いろいろと実験しながら楽しく学んでいけたらなんて思っています。

## figaでボタンを作る

こんなボタンコンポーネントを作ってみた。（↓figma）

![](/images/amplify-figma-study-01/2023-04-14-08-38-42.png)

## コンポーネントのプロパティ

コンポーネントに設定したプロパティは下記のようにしてみました。
これは、`MyButtonFixed`、`MyButtonHug`どちらも同じです。

| プロパティ| 値 | 説明 |
| --- | --- | --- |
| State | Default | デフォルト |
|       | Pressed | ボタンが押された時のデザイン |
|       | Disable | ボタンが無効状態のデザイン |
| Round | true | ボタンの角が丸いデザイン |
|       | false | ボタンの角が`true`のときより丸みのないデザイン |

## コンポーネントの差異

コンポーネントの差異は、コンポーネントのボタン幅、高さが、固定幅（Fixed）かハグ（Hug）かどうかの違いです。
あとは全て同じ設定になっています。
このボタンコンポーネントを実際に画面に表示させていきます。

| MyButtonFixed | MyButtonHug |
| --- | --- |
| ![](/images/amplify-figma-study-01/2023-04-14-08-45-38.png) | ![](/images/amplify-figma-study-01/2023-04-14-08-46-27.png) |

これをみてわかる通り、（まぁ複製して作ったので）構造は全く同じ。

## Amplify Studioに取り込んでみよう

コンポーネントが作成できたので、`Amplify Studio`に取り込んでみます。

プレビュー機能が割としっかりプレビューしてくれるので、プレビューで出来栄えを確認します。
`State`を変更してみると、しっかり色味が変わってくれます。

* MyButtonFixed（State='Default', Rounded='false'）
![](/images/amplify-figma-study-01/2023-04-14-08-47-57.png)
* MyButtonFixed（Pressed='Default', Rounded='false'）
![](/images/amplify-figma-study-01/2023-04-14-08-48-24.png)
* MyButtonFixed（Disabled='Default', Rounded='false'）
![](/images/amplify-figma-study-01/2023-04-14-08-49-12.png)

`Round`の方も変わってくれています。
（最初に作ったときにバリアントの設定ミスがあったため、表示できていなかったのが左側）

* MyButtonFixed（Default='Default', Rounded='true'）
![](/images/amplify-figma-study-01/2023-04-14-08-51-53.png)
* MyButtonFixed（Pressed='Default', Rounded='true'）
![](/images/amplify-figma-study-01/2023-04-14-08-53-08.png)
* MyButtonFixed（Disabled='Default', Rounded='true'）
![](/images/amplify-figma-study-01/2023-04-14-08-53-23.png)

これで`State`×`Round`の組み合わせ6通りが確認できました。

* MyButtonHug（State='Default', Rounded='false'）
![](/images/amplify-figma-study-01/2023-04-14-08-55-19.png)
* MyButtonHug（State='Pressed', Rounded='false'）
![](/images/amplify-figma-study-01/2023-04-14-08-55-36.png)
* MyButtonHug（State='Disabled', Rounded='false'）
![](/images/amplify-figma-study-01/2023-04-14-08-55-51.png)
* MyButtonHug（State='Default', Rounded='true'）
![](/images/amplify-figma-study-01/2023-04-14-08-54-28.png)
* MyButtonHug（State='Pressed', Rounded='true'）
![](/images/amplify-figma-study-01/2023-04-14-08-54-45.png)
* MyButtonHug（State='Disabled', Rounded='true'）
![](/images/amplify-figma-study-01/2023-04-14-08-55-00.png)

ボタンを各組み合わせ表示してみると、こんな結果に。
上の6つは`MyButtonFixed`なので、figmaで固定した W:91px H:40px になっています。
下の6つは`MyButtonHug`で、こちらは幅いっぱいに伸びてしまいました。


![](/images/amplify-figma-study-01/2023-04-14-12-40-20.png)

今度は`<Flex>`に囲んで横揃えにしてみました。

```tsx test.tsx
<View style={{ padding: "10px" }}>
  <Flex direction="column">
    <Text textAlign="left">MyButtonFixed:</Text>
    <Flex>
      <MyButtonFixed state="Default" rounded="true" />
      <MyButtonFixed state="Pressed" rounded="true" />
      <MyButtonFixed state="Disabled" rounded="true" />
      <MyButtonFixed state="Default" rounded="false" />
      <MyButtonFixed state="Pressed" rounded="false" />
      <MyButtonFixed state="Disabled" rounded="false" />
    </Flex>
    <Text textAlign="left">MyButtonHug:</Text>
    <Flex>
      <MyButtonHug state="Default" rounded="true" />
      <MyButtonHug state="Pressed" rounded="true" />
      <MyButtonHug state="Disabled" rounded="true" />
      <MyButtonHug state="Default" rounded="false" />
      <MyButtonHug state="Pressed" rounded="false" />
      <MyButtonHug state="Disabled" rounded="false" />
    </Flex>
  </Flex>
</View>
```

![](/images/amplify-figma-study-01/2023-04-14-12-43-02.png)

横に並べると、どっちも同じサイズ（W:80px, H:40px）に！
この差は一体何？？
実際に`amplify pull`を行なって生成された`MyButtonFixed.jsx`と`MyButtonHug.jsx`を比較してみると、次のことがわかりました。

```diff tsx
  // MyButtonFixed.jsx
  return (
    <Flex
      gap="8px"
      direction="row"
-      width="91px"
-      height="40px"
      justifyContent="flex-start"
        .
        .
        （省略）
---
  // MyButtonHug.jsx
  return (
    <Flex
      gap="8px"
      direction="row"
+      width="unset"
+      height="unset"
      justifyContent="flex-start"
        .
        .
        （省略）
```

`width`と`height`の値に差異が見られました。
まぁこれは、figmaでの設定通りといえば通りですね。
でも、縦に並べたときはなんで幅いっぱいに伸びちゃうんだろう・・

> unset は CSS のキーワードで、プロパティをリセットし、親から自然に継承された場合は継承値、そうでなければ初期値を設定します。言い換えれば、前者の継承プロパティの場合は inherit キーワードのように動作し、後者の非継承プロパティの場合は initial キーワードのように動作します。
> 
> unset は一括指定の all を含む、あらゆる CSS プロパティに対して適用することができます。

（https://developer.mozilla.org/ja/docs/Web/CSS/unset より）

ちょっと理解できているか自信ないけど、要は親によって変わるのね。

## まとめ
というわけで、figmaでボタンレイアウトを作成してみましたが、単品で使う分にはまぁまぁ分かってきたような、まだ分かっていないような。。
でも、きっちりボタンサイズが決まっている場合は、figma上で固定で指定しまった方が楽な気がします。
レスポンシブ対応をしなければいけないときは、デザイン上はハグにしておいて、調整するという手もありかもですね。


## 参考リンク
[CSS値の「initial」「inherit」「unset」「revert」の違い](https://qiita.com/h-naito/items/3027f92dde68899159c7)
