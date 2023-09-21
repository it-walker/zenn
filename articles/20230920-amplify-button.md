---
title: "Amplifyのボタンのレイアウトに潜入調査"
emoji: "👋"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "UI", "Button"]
published: true
---

## Amplifyのボタンレイアウトを考える
Amplifyを使うと、Figmaをうまく利用することで、CSSを書く頻度がだいぶ少なくなります。
極論、CSSをどこまで書かずにできるのかを研究していきたいんですよね。

というわけで、ここでは、

* CSSは使わず、①Figmaのテーマ設定、②コンポーネントで指定できるところまで（htmlに直書きはなし）

という掟を作って研究を進めていきたいわけです。

本日は、まぁよく使うであろう`ボタン`コンポーネントについて調べてきたのでこちらについて語っていきたいと思います。


## ボタンコンポーネントのバリエーションについて

公式ドキュメントのボタンの種類としては、5種類＋デフォルトで計6種類あるようです。

figmaのButtonコンポーネントのvariant型一覧（@aws-amplify/ui-react: 4.6.5）

![](/images/20230920-amplify-button/2023-09-20-18-30-52.png)

公式ドキュメントより、5種類。あと`default`もあるはずなので、計6種類というわけ。

![](/images/20230920-amplify-button/2023-09-20-18-24-19.png)


## ボタンの配色について

色々調べていくと、まず、色使いなどの設定の優先順位があるようでして、まぁ、ここはだいたい想像つくかと思いますが、`個別設定＞共通設定`といった関係性になります。
したがって、個別設定では、変更したい部分の設定がなされていて、それ以外は、デフォルトのボタンレイアウトになるという構成となっているようです。

例えば、フォントサイズや、ボーダーなどは、ボタンのバリエーションごとに設定が設けられているということはなく、デフォルトボタンの方で定義されています。

ボタンの配色については、下記の6種類が定義されています。
※primaryカラーは緑っぽいものになっています。それ以外はデフォルトのものを使用しています

| Buttonのvariation | default | hover | active | focus |
| --- | --- | --- | --- | --- |
| default | ![](/images/20230920-amplify-button/2023-09-20-18-39-51.png) | ![](/images/20230920-amplify-button/2023-09-20-18-43-53.png) | ![](/images/20230920-amplify-button/2023-09-20-18-45-54.png) | ![](/images/20230920-amplify-button/2023-09-20-18-47-58.png) |
| destructive | ![](/images/20230920-amplify-button/2023-09-20-18-40-08.png) | ![](/images/20230920-amplify-button/2023-09-20-18-44-09.png) | ![](/images/20230920-amplify-button/2023-09-20-18-46-11.png) | ![](/images/20230920-amplify-button/2023-09-20-18-48-19.png) |
| link | ![](/images/20230920-amplify-button/2023-09-20-18-40-54.png) | ![](/images/20230920-amplify-button/2023-09-20-18-44-22.png) | ![](/images/20230920-amplify-button/2023-09-20-18-46-25.png) | ![](/images/20230920-amplify-button/2023-09-20-18-48-35.png) |
| menu | ![](/images/20230920-amplify-button/2023-09-20-18-41-06.png) | ![](/images/20230920-amplify-button/2023-09-20-18-44-40.png) | ![](/images/20230920-amplify-button/2023-09-20-18-46-38.png) | ![](/images/20230920-amplify-button/2023-09-20-18-48-48.png) |
| primary | ![](/images/20230920-amplify-button/2023-09-20-18-41-21.png) | ![](/images/20230920-amplify-button/2023-09-20-18-44-53.png) | ![](/images/20230920-amplify-button/2023-09-20-18-46-54.png) | ![](/images/20230920-amplify-button/2023-09-20-18-49-00.png) |
| warning | ![](/images/20230920-amplify-button/2023-09-20-18-41-31.png) | ![](/images/20230920-amplify-button/2023-09-20-18-45-05.png) | ![](/images/20230920-amplify-button/2023-09-20-18-47-06.png) | ![](/images/20230920-amplify-button/2023-09-20-18-49-12.png) |


この結果を見てみると分かる通り、設定したプライマリーカラーはいろんな箇所に反映されそうですね。
元々の設定で`primary.〜`を参照しているということが分かると思います。


## ボタンレイアウトについて

下記の公式ドキュメントを見てみると、詳細が分かるのですが、なにせいっぱい設定項目があるので、ここでは絞りに絞ってお伝えしていこうと思います。
https://ui.docs.amplify.aws/angular/theming/css-variables

下の表は、ボタンのバリアントごとにどういう設定を参照しているのかをまとめたものになります。
1つ1つ確認しては見たのですが、見落としたりしている可能性もありますので、あくまで参考程度に見ていただけると嬉しいです（汗

※空欄については、未設定項目となります。したがって、デフォルトで設定している値が適用されることになります
※`個別設定＞共通設定`という関係性なので、競合している設定については、個別で指定している設定がイキとなります。この辺りはCSSとおんなじノリですかね・・
※CSSの変数名をそのまま載せたらめちゃめちゃ見づらかったので、省略しています（「--amplify-components」部分を省いています）


| 項目 | default | destructive | link | menu | primary | warning |
| --- | --- | --- | --- | --- | --- | --- |
| color | var(--color) | var(--destructive-color)<br>→var(--colors-font-inverse) | var(--link-color)<br>→var(--colors-font-interactive) |  | var(--primary-color)<br>→var(--colors-font-inverse) | var(--warning-color)<br>→var(--colors-red-60) |
| borderColor | var(--border-color) | var(--destructive-border-color)<br>→transparent |  |  | var(--primary-border-color)<br>→transparent | var(--warning-border-color)<br>→var(--colors-red-60) |
| backgroundColor | buttonface | var(--destructive-background-color)<br>→var(--colors-red-60) | var(--link-background-color)<br>→transparent | var(--menu-background-color)<br>→transparent | var(--primary-background-color)<br>→var(--colors-brand-primary-80) | var(--warning-border-color)<br>→transparent |
| borderRadius | var(--border-radius) |  |  |  |  |  |
| borderStyle | var(--border-style) |  |  |  |  |  |
| borderWidth | var(--border-width) | var(--destructive-border-width)→var(--border-widths-small) | var(--link-border-width)<br>→0※線幅0なので、罫線が発生しない | var(--menu-border-width)<br>→0※線幅0なので、罫線が発生しない | var(--primary-border-width)<br>→var(--border-widths-small) | var(--warning-border-width)<br>→var(--border-widths-small) |
| fontSize | var(--font-size) |  |  |  |  |  |
| color（hover） |  | var(--destructive-hover-color)<br>→var(--colors-font-inverse) | var(--link-hover-color)<br>→var(--colors-font-hover) | var(--menu-hover-color)<br>→var(--colors-font-inverse) | var(--primary-hover-color)<br>→var(--colors-font-inverse) | var(--warning-hover-color)<br>→var(--colors-font-error) |
| backgroundColor（hover） |  | var(--destructive-hover-background-color)<br>→var(--colors-red-80) | var(--link-hover-background-color)<br>→var(--colors-brand-primary-10) | var(--menu-hover-background-color)<br>→var(--colors-brand-primary-80) | var(--primary-hover-background-color)<br>→var(--colors-brand-primary-90) | var(--warning-hover-background-color)<br>→var(--colors-red-10) |
| borderColor（hover） |  | var(--destructive-hover-border-color)<br>→transparent | var(--link-hover-border-color)<br>→transparent |  | var(--primary-hover-border-color)<br>→transparent | var(--warning-hover-border-color)<br>→var(--colors-red-80) |
| color（focus） |  | var(--destructive-focus-color)<br>→var(--colors-font-inverse) | var(--link-focus-color)<br>→var(--colors-font-focus) | var(--menu-focus-color)<br>→var(--colors-font-inverse) | var(--primary-focus-color)<br>→var(--colors-font-inverse) | var(--warning-focus-color)<br>→var(--colors-red-80) |
| backgroundColor（focus） |  | var(--destructive-focus-background-color)<br>→var(--colors-red-80) | var(--link-focus-background-color)<br>→var(--colors-brand-primary-10) | var(--menu-focus-background-color)<br>→var(--colors-brand-primary-80) | var(--primary-focus-background-color)<br>→var(--colors-brand-primary-90) | var(--warning-focus-background-color)<br>→var(--colors-red-10) |
| borderColor（focus） |  | var(--destructive-focus-border-color)<br>→transparent | var(--link-focus-border-color)<br>→transparent |  | var(--primary-focus-border-color)<br>→transparent | var(--warning-focus-border-color)<br>→var(--colors-red-80) |
| boxShadow（focus）
※focusだけboxShadowがある |  | var(--destructive-focus-box-shadow)<br>→var(--fieldcontrol-error-focus-box-shadow)<br>→0px 0px 0px 1px var(--colors-border-error) | var(--link-focus-box-shadow)<br>→var(--fieldcontrol-focus-box-shadow)→0px 0px 0px 1px var(--colors-border-focus)<br>→var(--colors-brand-primary-100) | none | var(--primary-focus-box-shadow)<br>→var(--fieldcontrol-focus-box-shadow)<br>→0px 0px 0px 1px var(--colors-border-focus)<br>→var(--colors-brand-primary-100) | var(--warning-focus-box-shadow)<br>→var(--fieldcontrol-error-focus-box-shadow)<br>→0px 0px 0px 1px var(--colors-border-error) |
| color（active） |  | var(--destructive-active-color)<br>→var(--colors-font-inverse)<br>→var(--colors-white) | var(--link-active-color)<br>→var(--colors-font-active)→var(--colors-brand-primary-100) | var(--menu-active-color)<br>→var(--colors-font-inverse)<br>→var(--colors-white) | var(--primary-active-color)<br>→var(--colors-font-inverse)<br>→var(--colors-white) | var(--warning-active-color)→var(--colors-red-100) |
| backgroundColor（active） |  | var(--destructive-active-background-color)<br>→var(--colors-red-100) | var(--link-active-background-color)<br>→var(--colors-brand-primary-20) | var(--menu-active-background-color)<br>→var(--colors-brand-primary-90) | var(--primary-active-background-color)<br>→var(--amplify-colors-brand-primary-100) | var(--warning-active-border-color)<br>→var(--amplify-colors-red-20) |
| borderColor（active） |  | var(--destructive-active-border-color)<br>→transparent | var(--link-active-border-color)<br>→transparent |  | var(--primary-active-border-color)<br>→transparent | var(--warning-active-border-color)<br>→var(--amplify-colors-red-100) |
| color（disabled） |  | var(--amplify-internal-disabled-color)<br>→var(--destructive-disabled-color) | var(--amplify-internal-disabled-color) | var(--amplify-internal-disabled-color) | var(--amplify-internal-disabled-color) | var(--amplify-internal-disabled-color) |
| backgroundColor（disabled） |  | var(--amplify-internal-disabled-background-color)<br>→var(--destructive-disabled-background-color) | var(--amplify-internal-disabled-background-color) | var(--amplify-internal-disabled-background-color) | var(--amplify-internal-disabled-background-color) | var(--amplify-internal-disabled-background-color) |
| borderColor（disabled） |  | var(--amplify-internal-disabled-border-color) | var(--amplify-internal-disabled-border-color) | var(--amplify-internal-disabled-border-color) | var(--amplify-internal-disabled-border-color) | var(--amplify-internal-disabled-border-color) |


