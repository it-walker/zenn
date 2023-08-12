---
title: "Amazon Pinpointのハンズオンをやってみた（その７）"
emoji: "👌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Pinpoint", "Handson"]
published: true
---

## はじめに

Amazon Pinpointのハンズオン７回目をお送りします。
`Eメールのキャンペーン作成`をやっていきたいと思います。

## Amazon Pinpoint のキャンペーンとは
> キャンペーンは、特定のセグメントをエンゲージするためのメッセージングの仕組みです。キャンペーンは、定義したスケジュールに従って、カスタマイズされたメッセージを送信します。コンソールを使用して、Amazon Pinpoint でサポートされているチャネル（Push通知、E メール、SMS など）を通じてメッセージを送信するキャンペーンを作成することができます。

## ハンズオンのURL
https://catalog.workshops.aws/amazon-pinpoint-customer-experience/ja-JP/email-template-and-campaign/create-email-campaign

## Eメールのキャンペーン設定

このハンズオンでは、35歳以上の全ての顧客に、ウェルカムメールのキャンペーンを即座に送信します。
→あれ？35歳を超える顧客に対する設定をしていたような・・まぁハンズオンだからいいか

`Amazon Pinpoint`ページの`キャンペーン`を選択して、`キャンペーンを作成`ボタンをクリックします。

![](/images/aws-pinpoint-handson-07/2023-08-13-05-36-01.png)

キャンペーン名は任意なので、ハンズオンに従って、`welcome_campaign`と入力します。

キャンペーンタイプは`標準キャンペーン`を選択します。

チャネルは`Eメール`を選択して、`次へ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-07/2023-08-13-05-40-53.png)

セグメントのプルダウンから、`older_than_35`へ選択し、`次へ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-07/2023-08-13-05-43-13.png)

Eメールテンプレートに作成ずみのテンプレートを選択します。

![](/images/aws-pinpoint-handson-07/2023-08-13-05-49-55.png)


そして、`次へ`ボタンをクリックします。


![](/images/aws-pinpoint-handson-07/2023-08-13-05-51-18.png)

キャンペーンを送信するタイミングは`即時`にして、`次へ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-07/2023-08-13-05-52-44.png)

![](/images/aws-pinpoint-handson-07/2023-08-13-05-55-03.png)

設定内容を確認して、`キャンペーンを起動`ボタンをクリックします。

![](/images/aws-pinpoint-handson-07/2023-08-13-05-56-58.png)


![](/images/aws-pinpoint-handson-07/2023-08-13-05-57-53.png)

これでキャンペーンの作成は完了しました。
少しすると、ステータスが`完了`になったのでここまでは順調！
次回は`ジャーニーの作成`をやっていきます。
ジャーニーって何？状態ですが、次回が楽しみです。
