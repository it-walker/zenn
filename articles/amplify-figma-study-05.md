---
title: "[Amplify-Figma#02] Text Fieldのカスタマイズ"
emoji: "🕌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Figma"]
published: true
---

## はじめに

さて、前回は figma コンポーネントを作成して、`Text Field`のエラー時の枠の色を変更しました。

![](/images/amplify-figma-study-05/2023-09-23-17-11-07.png)

今回は、エラー時の枠をもう少し強調したいのと、エラーメッセージの文字色を枠の色に合わせて行こうと思います。

## Text Field をもう少し眺めてみる

さて、ここでふと思いました。
「あれ！？罫線の太さはどこで変えるんだ？？」と。

![](/images/amplify-figma-study-05/2023-09-23-17-22-14.png)

Figma で見る限り、そんな設定がないのよね。
なので画面の方を見てみる。

![](/images/amplify-figma-study-05/2023-09-23-17-23-33.png)

エラー時の罫線色は`.amplify-input--error`内で設定しているので、これは限定的な使い方だよね。
でも、`.amplify-input`クラスに設定されている`border-width`は、エラー時だけじゃなくて通常時にも影響を受けちゃうので、ここを変えるわけにはいかない。

```styles.css
.amplify-input {
    box-sizing: border-box;
    color: var(--amplify-components-fieldcontrol-color);
    font-size: var(--amplify-components-fieldcontrol-font-size);
    line-height: var(--amplify-components-fieldcontrol-line-height);
    padding-block-start: var(--amplify-components-fieldcontrol-padding-block-start);
    padding-block-end: var(--amplify-components-fieldcontrol-padding-block-end);
    padding-inline-start: var(--amplify-components-fieldcontrol-padding-inline-start);
    padding-inline-end: var(--amplify-components-fieldcontrol-padding-inline-end);
    transition: all var(--amplify-components-fieldcontrol-transition-duration);
    width: 100%;
    border-color: var(--amplify-components-fieldcontrol-border-color);
    border-radius: var(--amplify-components-fieldcontrol-border-radius);
    border-style: var(--amplify-components-fieldcontrol-border-style);
    border-width: var(--amplify-components-fieldcontrol-border-width);
    outline-color: var(--amplify-components-fieldcontrol-outline-color);
    outline-style: var(--amplify-components-fieldcontrol-outline-style);
    outline-width: var(--amplify-components-fieldcontrol-outline-width);
    outline-offset: var(--amplify-components-fieldcontrol-outline-offset);
    -webkit-user-select: text;
    user-select: text;
    display: inline-block;
    --amplify-components-fieldcontrol-color: var( --amplify-components-input-color );
    --amplify-components-fieldcontrol-border-color: var( --amplify-components-input-border-color );
    --amplify-components-fieldcontrol-font-size: var( --amplify-components-input-font-size );
    --amplify-components-fieldcontrol-focus-border-color: var( --amplify-components-input-focus-border-color );
}
```

TextField に直接`@borderWidth`を設定しても変わってくれない。うーん。。

```diff
  ErrorQuietTextField: {
    isDisabled: isDisabled,
    errorMessage: "エラーメッセージ",
    hasError: true,
+   borderWidth: "5px",
  }
```

## 公式ドキュメントを眺めてみる

公式ドキュメントを眺めていくと、おおっ！あるじゃんいいのが。
`@inputStyle`というプロパティがありました。

> Using style props:
>
> All style props will be applied to the Flex wrapper of the TextField. To style the input > of the TextField, you can pass a inputStyles prop with the style props you want to apply > to the input.
>
> （翻訳 ↓）
>
> スタイルの小道具を使う
>
> すべてのスタイル・プロップスは、TextField の Flex ラッパーに適用されます。TextField の入力をスタイル > するには、入力に適用したいスタイル > プロップを inputStyles プロップに渡します。

https://ui.docs.amplify.aws/react/components/textfield#local-styling

これを試してみましょう。

```diff
+  // なるべくamplifyの色を使うようにしたいので、テーマの中から使用するようにする
+  const { tokens } = useTheme()
+  // あとで使いまわせるように変数化しておく
+  const errorStyle: BaseStyleProps = {
+    borderWidth: tokens.borderWidths.medium
+  }
  .
  .
  .
  ErrorQuietTextField: {
    isDisabled: isDisabled,
    errorMessage: "エラーメッセージ",
    hasError: true,
+   inputStyles: errorStyle,
  }
```

![](/images/amplify-figma-study-05/2023-09-23-18-05-01.png)

太くなりましたー！しかもエラー時だけになっているので、これならうまく使えそう。
ついでにちょっと背景色も入れちゃおっかなー

追加するのは下記の１行。これも amplify のテーマから pink[10]を設定します。

```diff
  const { tokens } = useTheme()
  const errorStyle: BaseStyleProps = {
    borderWidth: tokens.borderWidths.medium,
+   backgroundColor: tokens.colors.pink[10]
  }
```

![](/images/amplify-figma-study-05/2023-09-23-18-07-27.png)

## エラー時のフォントは？

![](/images/amplify-figma-study-05/2023-09-23-18-11-52.png)

これを深ぼっていくと、`--amplify-colors-font-error`の色設定が効いているようです。
これは、名称的にエラー時の文字色に該当しそうなので、おんなじ赤でもよさそうですよね。

これは Figma から変更できそうです。

![](/images/amplify-figma-study-05/2023-09-23-18-14-15.png)

色の設定が変わっただけだと差分が出ない！！

![](/images/amplify-figma-study-05/2023-09-23-18-16-57.png)

変更を取り込んで実行してみると、無事に変更できていました！

![](/images/amplify-figma-study-05/2023-09-23-18-21-06.png)

## さいごに

今回は、どうにか予定していた TextField のエラー時のスタイリングをすることができました。
もっと細かいところを変更しようとするとまた問題が出てきそうではありますが、少しずつ Amplify を理解して最適解を探していきたいと思います。

にしてもここまで CSS 使ってないですからね。figma で直感的にオブジェクトを配置するだけでここまでできるのはすごいなぁと思いました。

次は何やろうかなぁ^^まだ思いついてないので、思いついたらまた筆をとっていきたいと思います。
次回もお楽しみに。
