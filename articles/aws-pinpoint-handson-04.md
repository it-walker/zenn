---
title: "Amazon Pinpointのハンズオンをやってみた（その４）"
emoji: "📘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Pinpoint", "Handson"]
published: true
---

## はじめに

Amazon Pinpointのハンズオンの４回目をお送りします。
`Amazon S3イベント通知を使用したエンドポイントの自動インポート`をやっていきたいと思います。

イメージはこんな感じなんですって。

![](/images/aws-pinpoint-handson-04/2023-08-12-15-53-38.png)



## ハンズオンのURL
https://catalog.workshops.aws/amazon-pinpoint-customer-experience/ja-JP/import-customers/Amazon-S3-Triggered-Endpoint-Imports


## ソリューションのデプロイ
まずは`AWS CloudFormation`を使用して、このソリューションをAWSアカウントにデプロイするんですって。

その前に`S3`に使用するCSVを保存するためのバケットを作成します。
（バケットの作成手順についてはここでは割愛します）

次に`CoudFormation`にいきましょう。
`スタックの作成`ボタンをクリックします。

![](/images/aws-pinpoint-handson-04/2023-08-12-16-00-55.png)

下記のリンクにあるテンプレートをあらかじめダウンロードしておきます。

[CloudFormationテンプレート](https://github.com/aws-samples/digital-user-engagement-reference-architectures/blob/master/cloudformation/Amazon_S3_triggered_import.yaml)

ダウンロードしたら、そのファイルをアップロードします。

![](/images/aws-pinpoint-handson-04/2023-08-12-16-02-37.png)

スタックの名前は`pinpont-customer-s3-import`とします。
`S3バケットは`先ほど作成したバケット名を入力します。
`PinpointProjectId`は大将プロジェクトのIDを入力します。

入力し終わったら`次へ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-04/2023-08-12-16-05-26.png)

スタックオプションの設定画面はそのまま`次へ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-04/2023-08-12-16-08-59.png)

最後のページは、一番下までスクロールしたら、`AWS CloudFormation によって IAM リソースが作成される場合があることを承認します。`というチェックボックスにチェックを入れ、`送信`ボタンをクリックします。

![](/images/aws-pinpoint-handson-04/2023-08-12-16-10-52.png)

![](/images/aws-pinpoint-handson-04/2023-08-12-16-09-38.png)

少し時間がかかるので、このまま処理が終わるまで待ちます。

![](/images/aws-pinpoint-handson-04/2023-08-12-16-12-13.png)

`CREATE_COMPLETE`が表示されればOKです。

![](/images/aws-pinpoint-handson-04/2023-08-12-16-14-17.png)

下記をダウンロードし、メールアドレスを更新します。

[sample.csv](https://static.us-east-1.prod.workshops.aws/public/301678ed-0734-4951-9d1d-027e8c96d15d/static/import_customers/S3_upload_segment_csv.csv)

S3バケットに移動し、上記のCSVをアップロードします。

![](/images/aws-pinpoint-handson-04/2023-08-12-16-15-25.png)

CSVのアップロードが完了したら、`Amaozn Pinpoint`のコンソールに移動し、`すべてのプロジェクト > プロジェクトの選択 > セグメント`に移動します。
対象のCSVファイル名で`インポート済み`タイプのセグメントが１行表示されます。

![](/images/aws-pinpoint-handson-04/2023-08-12-16-17-32.png)


というわけで、まだ言われた通りに作業しているだけなので、なんとなくしか理解できていませんが、どうにかここまでの作業を完了することができました。

さて次回は、`動的セグメントの構築`をやっていきます。
それではまた！
