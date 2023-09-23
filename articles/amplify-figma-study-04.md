---
title: "[Amplify-Figma#01] Figmaコンポーネントを作ってText Fieldのエラー時の赤の色を変更してみる"
emoji: "🕌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Figma"]
published: true
---

## はじめに

今回は、せっかく figma が使えるので、figma を使ったコンポーネントを作成していきたいと思います。
その中で、主にカラー設定のところを見ていきます。
どの設定をいじるとどこに影響するのか。この辺りが少しわかってくるといいなぁと思います。

## Figma でコンポーネント

かんたんですが、前に実装したものと同じようなものを、今度は figma で作ってみようと思いました。

fimga で作ったコンポーネントはこちらです。

![](/images/amplify-figma-study-04/2023-09-23-15-21-52.png)

figma を作成したら、`Sync with Figma`を実行します。

![](/images/amplify-figma-study-04/2023-09-23-15-23-19.png)

コンポーネントが`Amplify Studio`に取り込まれたので、ローカルに落とし込みます。

```
amplify pull -y
```

これで取り込みは完了。
次に`isDisabled`のイベント発火と`Text Field`をエラー状態にしておきたいので、エラー状態にするように、取り込んだコンポーネントをオーバーライドする形で実装を加えていきます。

```TestPage.tsx
import { useState } from "react"
import { TestComponent } from "../../ui-components"

export default function TestPage() {
  const [isDisabled, setIsDisabled] = useState(false)
  return (
    <TestComponent
      overrides={{
        ActiveControlSwitchField: {
          isChecked: isDisabled,
          onChange: () => {
            setIsDisabled(!isDisabled)
          },
        },
        DefaultButton: {
          isDisabled: isDisabled
        },
        DestructiveButton: {
          isDisabled: isDisabled
        },
        LinkButton: {
          isDisabled: isDisabled
        },
        PrimaryButton: {
          isDisabled: isDisabled
        },
        WarningButton: {
          isDisabled: isDisabled
        },
        DefaultTextField: {
          isDisabled: isDisabled
        },
        QuietTextField: {
          isDisabled: isDisabled
        },
        ErrorDefaultTextField: {
          errorMessage: "エラーメッセージ",
          hasError: true,
          isDisabled: isDisabled,
        },
        ErrorQuietTextField: {
          isDisabled: isDisabled,
          errorMessage: "エラーメッセージ",
          hasError: true,
        }
      }}
    >
    </TestComponent>)
}
```

これをローカルで動かしてみると、こうなります。

![](/images/amplify-figma-study-04/2023-09-23-15-49-03.png)

## ここからちょっとカスタマイズしていきたい

エラー時の赤をもう少し明るめにしたいんですよね。
あと、文字も弱いのでもう少し太めにして目立たせたい。
テキストボックスの赤い枠ももう少し太くしたほうがいいかしら。

![](/images/amplify-figma-study-04/2023-09-23-15-50-01.png)

とちょっと欲が出てきたので、このあたりから攻めていきたいと思いますよ。
まずは、色を変えてみますか。

エラー状態にすると、テキストボックスには、下記の CSS が有効になるようです。

![](/images/amplify-figma-study-04/2023-09-23-15-51-50.png)

```styles.css
.amplify-input--error {
    border-color: var(--amplify-components-fieldcontrol-error-border-color);
}
```

`border-color`なので、まさしくエラー時の罫線に当たる部分の色の設定になりますね。

`--amplify-components-fieldcontrol-error-border-color`をもう少し深掘りしていきます。
`--amplify-colors-border-error`

![](/images/amplify-figma-study-04/2023-09-23-15-55-52.png)

```
--amplify-components-fieldcontrol-error-border-color: var(--amplify-colors-border-error);
```

というわけで、`amplify-colors-border-error`に設定されている色味を変更すればよさそうです。でも、名前から察するに、ここが設定されている部分の色が変わってしまうってことですよね！？
ちゃんと理解して使わないと怖いです・・

figma 上では、ハイフン区切りをピリオド`.`、または`/`で置き換えればよさそうです。
figma 上で`amplify.colors.border.error`を探してみましょう。

![](/images/amplify-figma-study-04/2023-09-23-15-58-58.png)

おおぅ、これっすね。
`{colors.red.80.value}`という記載になっているので、figma 上で定義されている赤色を使ってそうです。

![](/images/amplify-figma-study-04/2023-09-23-15-59-35.png)

ここでは、直接色を指定して変更しちゃいましょう。
ChatGPT にエラー時のおすすめ赤を提案してもらいました。
`#FF0000`とのことなので、これを指定してみます。

```
エラー表示におすすめの赤い色は、通常、注意を引きやすくするために明るく鮮やかな赤色が使われます。以下は16進数で表現した赤色の提案です。

色: #FF0000

この色がおすすめされる理由は次の通りです：

視覚的な注意: 赤色は一般的に人間の視覚に対して非常に目立ち、注意を引きます。エラーメッセージや警告の表示に赤色を使うことで、ユーザーが問題や注意事項に注意を向けるのに役立ちます。

標準的なカラーコード: #FF0000 はHTMLやCSSなどのウェブデザインにおいて一般的に使用される標準的な赤色のカラーコードです。このカラーコードは広く認識されており、使いやすいです。

感情的な意味合い: 赤色は危険やエラーなどのネガティブな感情や状況を示すのに適しています。ユーザーにとって、エラーや警告があることを知らせるのに赤色を使うことで、情報を素早く理解しやすくなります。

ただし、赤色を使う際には、適切なコントラスト比を確保し、視覚的なアクセシビリティを考慮することが重要です。特に、赤色は一部の視覚障害者にとって認識が難しいことがあるため、十分な対策を講じることが必要です。
```

![](/images/amplify-figma-study-04/2023-09-23-16-04-01.png)

`Update theme`をしたら、figma の編集はおしまい。`Amplify Studio`で`Sync with Figma`からの`amplify pull`しちゃいましょう。

![](/images/amplify-figma-study-04/2023-09-23-16-05-28.png)

差分もこの通り。
テーマ設定の json も書き変わってくれます。
テーマ設定上の色味は、全て`hsl()`で表現されるんですね。

![](/images/amplify-figma-study-04/2023-09-23-16-09-15.png)

では、ローカルで動かしてみましょう！
おっ枠は想定通り変わりましたね！

![](/images/amplify-figma-study-04/2023-09-23-16-14-02.png)

## さいごに

というわけで、今回は Figma で作ったコンポーネントを使って、カスタマイズをしていきました。
色の設定をもっと詳しくみていきたいので、色々と試しながら理解を深めていきたいと思います。

今回は、`Text Field`のエラー時のテキストボックス枠の色を変更しました。
罫線の太さとか、メッセージ部分の文字色なんかも変えていきたい！
欲張ると収拾つかなくなるので、今回はこの辺りでやめておきますが、また続きをしていけたらと思います。
