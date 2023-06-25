---
title: "[AWS Hands-on for Beginners]Serverlessのハンズオンを実際にやってみたよ（1）"
emoji: "💬"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS"]
published: true
---

## AWS Lambda ハンズオン① Lambda を単体で使ってみる

今回やってみたハンズオンは、`AWS Hands-on for Beginners 〜Serverless #1〜`でございます。
サーバーレスアーキテクチャ、実際に触ってみたことがあんまりないので試しにやってみました。

リンクはこちら↓

https://pages.awscloud.com/JAPAN-event-OE-Hands-on-for-Beginners-Serverless-1-2022-reg-event.html?trk=aws_introduction_page

## Lambdaファンクション作成

さっそく、Lambdaファンクションを作成しましょう。
右上の`関数の作成`ボタンをクリックします。

![](/images/aws-serverless-handson-01/2023-06-24-16-37-51.png)

今回は、`一から作成`を選びます。

![](/images/aws-serverless-handson-01/2023-06-24-16-38-28.png)

`関数名`には`translateFunction`としています。
そして`ランタイム`は`Python 3.10`を選択します。

![](/images/aws-serverless-handson-01/2023-06-24-16-39-43.png)

次に`実行ロール`です。
実行ロールについては、`基本的な Lambda アクセス権限で新しいロールを作成`を選ぶことにしました。
ここまでの設定が終わったら、`関数の作成`ボタンをクリックします。

![](/images/aws-serverless-handson-01/2023-06-24-16-40-00.png)

はい、あっという間に関数が出来上がり。

![](/images/aws-serverless-handson-01/2023-06-24-16-40-39.png)

最初に、テストを実施してみます。

![](/images/aws-serverless-handson-01/2023-06-24-16-43-15.png)

テスト結果はこちら。

![](/images/aws-serverless-handson-01/2023-06-24-16-44-04.png)

次に、ログを出力する処理を追加します。

![](/images/aws-serverless-handson-01/2023-06-24-16-46-56.png)

保存したら、再度テストを実施してみます。
パラメータが出力されるようになました。

![](/images/aws-serverless-handson-01/2023-06-24-16-51-55.png)


## 感想
まだ特に何かをする関数は作れていないけど、手軽に作れてしまうのはすごいですね。
使いこなせるようになると、ちょっとしたものはサクッと作れちゃうんだろうな・・

まだまだハンズオン、始まったばかりなので、この後も続き、やって行ってみたいと思います。
