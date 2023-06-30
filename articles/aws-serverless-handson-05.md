---
title: "[AWS Hands-on for Beginners]Serverlessのハンズオンを実際にやってみたよ（5）"
emoji: "📑"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "API", "DinamoDB"]
published: true
---

## Amazon DynamoDB ハンズオン① テーブルを作ってみる

それでは、続きをやっていきましょう。
今回は、DynamoDBのテーブルを作成していきます。

`テーブルの作成`ボタンをクリックします。

![](/images/aws-serverless-handson-05/2023-06-30-19-11-13.png)

![](/images/aws-serverless-handson-05/2023-06-30-19-16-00.png)

`テーブル名`を`translate-history`、`パーティションキー`は`timestamp`とし、`文字列`のままにします。


![](/images/aws-serverless-handson-05/2023-06-30-19-18-08.png)

`テーブル設定`については`設定をカスタマイズ`に変更します。

![](/images/aws-serverless-handson-05/2023-06-30-19-23-39.png)

`読み込み/書き込みキャパシティの設定`については、`キャパシティモード`を`プロビジョンド`に変更します。

`読み込みキャパシティ`は`オフ`で`プロビジョンドキャパシティユニット`は`1`にします。（今回はハンズオンなので）

`書き込みキャパシティ`も同様です。


![](/images/aws-serverless-handson-05/2023-06-30-19-25-01.png)

その他の設定は特に変更なしです。

![](/images/aws-serverless-handson-05/2023-06-30-19-28-55.png)

設定が完了したら`テーブルの作成`ボタンをクリックします。
これでテーブルの作成が開始されます。

![](/images/aws-serverless-handson-05/2023-06-30-19-29-22.png)

テーブル作成中です。

![](/images/aws-serverless-handson-05/2023-06-30-19-31-39.png)

テーブル作成が完了しました！

![](/images/aws-serverless-handson-05/2023-06-30-19-32-08.png)

次に、テーブル名`trans-history`を選択します。

![](/images/aws-serverless-handson-05/2023-06-30-19-35-10.png)

次に、項目の追加をしてみましょう。
`アクション>項目を作成`をクリックします。

![](/images/aws-serverless-handson-05/2023-06-30-19-35-48.png)


![](/images/aws-serverless-handson-05/2023-06-30-19-36-32.png)


![](/images/aws-serverless-handson-05/2023-06-30-19-37-44.png)

`timestamp`の値を入力していきます。
今回は、`202306391830000`を入力します。

![](/images/aws-serverless-handson-05/2023-06-30-19-39-35.png)


もう一つパラメータを追加します。
`新しい属性の追加>文字列`をクリックします。

![](/images/aws-serverless-handson-05/2023-06-30-19-41-15.png)

パラメータを`input_text`とし、値を`★こんにちは`と入力します。

![](/images/aws-serverless-handson-05/2023-06-30-19-41-54.png)


さらにもう1つ、`output_text`を追加します。
値には`★Hello`を入力します。
入力し終えたら`項目を作成`ボタンをクリックします。

![](/images/aws-serverless-handson-05/2023-06-30-19-44-02.png)

これで1つ、項目を追加することができました。

![](/images/aws-serverless-handson-05/2023-06-30-19-45-19.png)

手動ですが、これで項目が1つ登録できることが確認できました。
