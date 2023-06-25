---
title: "[AWS Hands-on for Beginners]Serverlessのハンズオンを実際にやってみたよ（3）"
emoji: "📘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "API", "Gateway"]
published: true
---

## Amazon API Gateway ハンズオン① API Gateway を単体で使ってみる

それでは、やっていきます。
まずは、`API Gateway`へ移動してみましょう。

![](/images/aws-serverless-handson-03/2023-06-25-18-05-47.png)

`Rest API`を使っていきます。
`構築`ボタンをクリックします。

`最初のAPIを作成する`という画面が出てくるので、`OK`ボタンをクリックします。

![](/images/aws-serverless-handson-03/2023-06-25-18-06-47.png)

`API 名`を適当に入力して、`APIの作成`ボタンをクリックします。
`エンドポイントタイプ`はデフォルトの`リージョン`のままいきます。

![](/images/aws-serverless-handson-03/2023-06-25-18-08-04.png)

作成が完了すると、下記の画面が表示されます。

![](/images/aws-serverless-handson-03/2023-06-25-18-08-50.png)

次に、リソースを作成します。
`アクション>リソースの作成`をクリックします。

![](/images/aws-serverless-handson-03/2023-06-25-18-09-11.png)

`リソース名`を入力します。
（`リソース名`を入力すると、`リソースパス`も自動的に入力されていきます。）
入力し終えたら、`リソースの作成`ボタンをクリックします。

![](/images/aws-serverless-handson-03/2023-06-25-18-09-41.png)

すると、`/リソース名`の項目が作成されます。
今回は`sample`としたので、`/sample`が作成されています。

![](/images/aws-serverless-handson-03/2023-06-25-18-10-11.png)

次に、`/sample`を選択した状態で、`アクション>メソッドの作成`をクリックします。

![](/images/aws-serverless-handson-03/2023-06-25-18-10-41.png)

`GETのセットアップ`画面が表示されます。


![](/images/aws-serverless-handson-03/2023-06-25-18-11-32.png)

今回はひとまずモックを作成していくので、`統合タイプ`は`Mock`を選択します。
その後、`保存`ボタンをクリックします。

![](/images/aws-serverless-handson-03/2023-06-25-18-11-52.png)

保存し終わると、`メソッドの実行`画面が表示されます。

![](/images/aws-serverless-handson-03/2023-06-25-18-12-11.png)

右下の`統合レスポンス`を選択します。

![](/images/aws-serverless-handson-03/2023-06-25-18-12-33.png)

`メソッドレスポンス`の設定を行っていきます。
`マッピングテンプレートの追加`をクリックします。

![](/images/aws-serverless-handson-03/2023-06-25-18-13-08.png)

入力テキストが表示されるので、`application/json`と入力して、作成します。

![](/images/aws-serverless-handson-03/2023-06-25-18-13-39.png)

すると、右側に`application/json`の入力欄が表示されるので、下記の内容を入力します。

```
{
  "statusCode": 200,
  "body": {
    "report_id": 5,
    "report_title": "Hello, World"
  },
  {
    "report_id": 7,
    "report_title": "こんにちは"
  }
}
```

入力し終えたら、`保存`ボタンをクリックします。

![](/images/aws-serverless-handson-03/2023-06-25-18-16-47.png)

準備が整ったので、`テスト`を実行してみましょう。
`テスト`ボタンをクリックします。

![](/images/aws-serverless-handson-03/2023-06-25-18-17-27.png)

テストを実行すると、先ほど作成したレスポンスが返却されました。

![](/images/aws-serverless-handson-03/2023-06-25-18-18-03.png)

次に、APIをデプロイしていきます。
`アクション>APIのデプロイ`をクリックします。

![](/images/aws-serverless-handson-03/2023-06-25-18-18-47.png)

`デプロイされるステージ`は新しく作成するので、`[新た強いステージ]`を選択します。
`ステージ名`は今回は`dev`としています。
入力し終えたら、`デプロイ`ボタンをクリックします。

![](/images/aws-serverless-handson-03/2023-06-25-18-19-25.png)

`dev ステージエディター`が作成されると、画面上側にURLが表示されています。
これが、作成したAPIのURLになります。

![](/images/aws-serverless-handson-03/2023-06-25-18-19-50.png)

リンクをクリックしてみると・・あれ？エラーになってる。
この手のエラーは、権限まわりかな？

![](/images/aws-serverless-handson-03/2023-06-25-18-20-03.png)

と思ったのですが、実行した場所が悪かったみたい。
先ほど作成したのは、`sample`のGETメソッドなので、下記の画面にあるURLが正しかった。

![](/images/aws-serverless-handson-03/2023-06-25-20-47-35.png)

URLをクリックしてみると、先ほど作成したレスポンスが返却されることが確認できました。
めでたしめでたし♪

![](/images/aws-serverless-handson-03/2023-06-25-20-48-49.png)

## さいごに

ここまでは、手を動かしてみてなんとなくわかってきました。
このハンズオンはもう少しあるので、まずは全ての単元をやり切って、もう少し込み入ったこともやってみたいですね。

