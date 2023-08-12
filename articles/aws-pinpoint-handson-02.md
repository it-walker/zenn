---
title: "Amazon Pinpointのハンズオンをやってみた（その２）"
emoji: "📘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Pinpoint", "Handson"]
published: true
---

## はじめに

Amazon Pinpointのハンズオンの２回目をお送りします。
準備が少しずつ整ってきて、データのインポートを行うところからスタートです。

## ハンズオンのURL
https://catalog.workshops.aws/amazon-pinpoint-customer-experience/ja-JP/prerequisites/create-a-project


## カスタマーデータのインポート
カスタマーデータをインポートするようです。
要は、ハンズオンなので、用意されたデータをインポートしてやってみようと理解。

サンプルデータはCSVで用意されていましたので、リンクを貼っておきます。

[sample.csv](https://static.us-east-1.prod.workshops.aws/public/301678ed-0734-4951-9d1d-027e8c96d15d/static/import_customers/console_upload_segment_csv.csv)

左メニューの`分析 > セグメント`をクリックします。
その後、`セグメントを作成`ボタンをクリックします。

![](/images/aws-pinpoint-handson-02/2023-08-12-14-40-04.png)

セグメント作成画面に遷移しました。

![](/images/aws-pinpoint-handson-02/2023-08-12-14-41-16.png)


`セグメントをインポート`を選択します。

![](/images/aws-pinpoint-handson-02/2023-08-12-14-41-48.png)


ダウンロードしたCSVをここで選択して、`セグメントを作成`ボタンをクリックします。

![](/images/aws-pinpoint-handson-02/2023-08-12-14-43-30.png)

これで、セグメントが正しく作成されたようです。

![](/images/aws-pinpoint-handson-02/2023-08-12-14-45-01.png)

aws pinpoint get-endpoint --application-id 1e0b081624214bef848c0a9a69a31f91 --endpoint-id 111

今回は、ちょっと早いですがここで終わりたいと思います。
次回は、`プログラムによるエンドポイントの作成`ということで、`Lambda Function`を使ったハンズオンになるようです。
それではまた次回！
