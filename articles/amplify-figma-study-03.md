---
title: "[Amplify×figma]コンポーネント化した部品のフォントファミリーを設定できるのかを調べてみた話"
emoji: "😽"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["amplify", "figma"]
published: true
---

## フォントファミリーの指定ってどうやんの？

機種によってフォントって依存してしまうよね。
そんなとき、フォントの優先順位を`font-family`で設定すると思うけど、figmaからどうやって設定するんだろうと思っていました。
というわけで、さっそく調べてみました。

`amplify pull`でコード化されたコンポーネントを見ると`fontFamily`に`Inter`って指定されちゃっているんだよね。
それだと困るんだけど、どうしたらいいんだろう。
→ゴシック系で画面表示したいのに、機種によっては、明朝体で表示されてしまったらダサいなぁ。

![](/images/amplify-figma-study-03/2023-04-15-21-40-30.png)

## テーマの設定でフォントファミリーの設定はできそう

こんな感じに設定すればフォントファミリーの優先順位の設定はできそうというところまでは分かりました。
ただ、各HTML要素で直接指定されているとなると、外からどう指定してもそっちの優先順位が勝ってしまう。。

```tsx
import { studioTheme } from './ui-components'
import { Theme, ThemeProvider } from '@aws-amplify/ui-react';

const theme: Theme = {
  ...studioTheme,
  name: 'custom-button-theme',
  tokens: {
    fonts: {
      default: {
        variable: {
          value: "'Helvetica', 'Arial', 'Yu Gothic UI', 'Hiragino Kaku Gothic ProN', 'Yu Gothic', 'Meiryo UI', 'Meiryo', 'Roboto', 'MS Gothic', 'MS PGothic', -apple-system, BlinkMacSystemFont;"
        },
        static: {
          value: "'Helvetica', 'Arial', 'Yu Gothic UI', 'Hiragino Kaku Gothic ProN', 'Yu Gothic', 'Meiryo UI', 'Meiryo', 'Roboto', 'MS Gothic', 'MS PGothic', -apple-system, BlinkMacSystemFont;"
        },
      },
    },
    .
    .
    （省略）

  return (
    <div className="App">
      <ThemeProvider theme={theme}>
      ・
      ・
      （省略）
```

ただ、これでも、Figma上で固定の文言を配置するときに、フォントを指定せざるを得ないんですよねー

![](/images/amplify-figma-study-03/2023-04-29-15-54-47.png)

いくら外側でフォントファミリーを指定しても、特定のテキストに対してフォントを設定しているので、優先順位が一番強い。。
Figma上で設定したフォントが入っていない別の端末だとどうなるかというと、どうやらWebブラウザのデフォルトフォントが設定されるようです。

Safariだと明朝体になっちまう・・・
iPhoneのsafariで表示させてみると下記のようになります。。
![](/images/amplify-figma-study-03/2023-04-29-15-59-42.png)


## プリミティブなコンポーネントはテーマの設定が活きそう
あらかじめ用意されている、プリミティブなコンポーネント（ボタン、テキストなど）については、Figma上でいくら何やっても設定が無視されます。

![](/images/amplify-figma-study-03/2023-04-29-16-02-44.png)

その代わり、プリミティブなコンポーネントについては、フォントファミリーの指定をしないので、上記のテーマ設定が効いてくるようです。
なので、フォントファミリーの指定をした順で端末にインストールされているフォントで表示してくれる。


## 結論

というわけで、今のところの結論です。

**Webフォントを使いなはれ**

### インストールさえしておけば、win/macの端末関係なくFigmaを編集できる
本件を調査している中で、win端末だと、Figmaが編集できないという問題にぶち当たりました。
もし、win/macどちらも同じように編集できるような環境を考えていくなら、テキストの編集時にフォントが欠落する、つまり、自端末にインストールされていないフォントが使用されていると、編集時に別のフォントに置き換えなければならないので、非常に扱いづらくなるということです。

というわけで、Figma編集環境を

①「Noto Sans CJK JP」を各自インストールする
②Figmaアプリを使用するようにする（ブラウザ版は使用しない）

この2点の制約をつけることで、どの環境下でも編集することができます。

### 実装もWebフォントを使う

`<head>〜</head>`にwebフォントの指定を入れておけば端末ごとの表示状態の心配がなくなります。
テーマの設定をしても、静的な固定文言が綺麗に表示できないので、この設定をしておけば心配な要素がなくなります。

```css
/** 例： Noto Sans Japaneseを使う場合 */
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@300;400;600&family=Zen+Kaku+Gothic+New&display=swap');
```

## さいごに
もっといいやり方があるかもしれませんが、色々と試してみた結果、この結論に至りました。
もし、「もっとこうした方がいいよ」と言ったご意見、ご感想などございましたら、ご指摘いただけますと幸いです。