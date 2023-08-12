---
title: "Amazon Pinpointのハンズオンをやってみた（その５）"
emoji: "💭"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Pinpoint", "Handson"]
published: true
---

## はじめに

Amazon Pinpointのハンズオンの５回目をお送りします。
`動的セグメントの構築`をやっていきたいと思います。

`35歳以上のすべてのユーザーを含む動的セグメント`を作成します。


## ハンズオンのURL
https://catalog.workshops.aws/amazon-pinpoint-customer-experience/ja-JP/import-customers/dynamic-segment

## 動的セグメントの作成

`セグメント`ページに遷移して、`セグメント`ボタンをクリックします。

![](/images/aws-pinpoint-handson-05/2023-08-12-17-38-20.png)


![](/images/aws-pinpoint-handson-05/2023-08-12-17-41-42.png)

セグメントの詳細の下に`other_than_35`と入力します。

![](/images/aws-pinpoint-handson-05/2023-08-12-17-42-45.png)

`基準を追加`ボタンをクリックして、属性を追加します。

![](/images/aws-pinpoint-handson-05/2023-08-12-17-43-46.png)

下記のように設定します。

| 項目 | 設定値 |
| --- | --- |
| 属性 | age |
| 演算子 | 超 |
| 値 | 35 |


![](/images/aws-pinpoint-handson-05/2023-08-12-17-46-33.png)


`セグメントを作成`ボタンをクリックします。

![](/images/aws-pinpoint-handson-05/2023-08-12-17-49-53.png)

`セグメントには複数のチャネルが含まれる場合があります`というダイアログが表示されますが、`了承しました`ボタンをクリックします。

これで、動的セグメントの作成が完了しました。

![](/images/aws-pinpoint-handson-05/2023-08-12-17-50-57.png)


今回の動的セグメントの作成はここまでとなります。
次回は、`パーソナライズされたEメールテンプレートによるキャンペーン`のハンズオンに進みます。
それでは、また次回！
