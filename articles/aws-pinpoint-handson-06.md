---
title: "Amazon Pinpointのハンズオンをやってみた（その６）"
emoji: "🌊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Pinpoint", "Handson"]
published: true
---

## はじめに

Amazon Pinpointのハンズオンの６回目をお送りします。
`Eメールテンプレートの作成`をやっていきたいと思います。


## ハンズオンのURL
https://catalog.workshops.aws/amazon-pinpoint-customer-experience/ja-JP/email-template-and-campaign/create-email-template

## Eメールのメッセージテンプレートの作成

`Amazon Pinpoint`ページの`メッセージテンプレート`を選択します。

![](/images/aws-pinpoint-handson-06/2023-08-12-18-00-17.png)

![](/images/aws-pinpoint-handson-06/2023-08-12-18-05-23.png)

テンプレート名に任意の名称を入力します。

![](/images/aws-pinpoint-handson-06/2023-08-12-18-07-57.png)

`属性ファインダーを開く`ボタンをクリックして、`カスタム属性 > カスタム属性を読み込む`をクリックします。

![](/images/aws-pinpoint-handson-06/2023-08-12-18-09-17.png)


![](/images/aws-pinpoint-handson-06/2023-08-12-18-10-21.png)


`Amazon Pinpoint`で作成したプロジェクト名にチェックを入れ、`カスタム属性を読み込む`ボタンをクリックします。

![](/images/aws-pinpoint-handson-06/2023-08-12-18-13-25.png)

これで、ユーザー属性がロードされ、表示されているユーザー属性をクリックすると、メッセージ変数がコピーされ、メールのHTML本文に貼り付けることができるとか。
やってみましょう。

件名を下記のように入力してみます。

```
**Welcome to Pinpoint {{User.UserAttributes.FirstName}}**
```

![](/images/aws-pinpoint-handson-06/2023-08-12-18-20-26.png)

次は本文を作成していきます。
サンプルが用意されているので、これを使います。

[メッセージ本文サンプル](https://static.us-east-1.prod.workshops.aws/public/301678ed-0734-4951-9d1d-027e8c96d15d/static/email_campaign/personalized_email_template.txt)

完成イメージがこちらになります。
`作成`ボタンをクリックして完了です。

![](/images/aws-pinpoint-handson-06/2023-08-12-18-23-44.png)

これで完成かと思いきや、何やらエラーが。
テンプレート名が競合してるとダメなのか・・

![](/images/aws-pinpoint-handson-06/2023-08-12-18-24-43.png)


でも、とりあえず問題なさそうだったので、そのままいきやす！
※テンプレート名の変更はできないので、変更したければ新しく作り直すしかなさそう・・


というわけで、今回はここまでにしたいと思います。
次回は、`Eメールのキャンペーン作成`をしていきたいと思います。
まだまだ先は長いなぁ・・でもがんばろー
