---
title: "Amazon Pinpointのハンズオンをやってみた（その９）"
emoji: "🌟"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Pinpoint", "Handson"]
published: true
---

## はじめに

Amazon Pinpointのハンズオン９回目をお送りします。
`イベントベースのジャーニー作成`をやっていきたいと思います。

## カスタムイベント
`AWS Lambda`と`Amazon Pinpoint Python SDKBoto3`を使って、カスタムイベントを記録します。前回作成したジャニーをコピーし、カスタムイベントに基づいてエンドポイントを処理します。

> Amazon Pinpoint では、モバイルアプリとウェブアプリの両方でカスタマーのイベントをトラッキングができます。これらのイベントはカスタムイベントと呼ばれ、Amazon Pinpoint のキャンペーンやジャーニーのイベントトリガーとして使用することができます。
> すべてのカスタムイベントはエンドポイントに関連付けられ、イベントの属性とメトリックを指定できます。例えば、カスタムイベント purchase は、属性 product とメトリック price を持つことができます。
> 記録されたカスタムイベントデータは、Amazon Pinpoint コンソール > あなたのプロジェクト(Your project) > 分析(Analytics) > イベント(Events) で確認することができます。最初にフィルタを有効にすることで、分析したいカスタムイベントを選択することができるようになります。
> カスタムイベントを記録するために、Amazon Pinpointは豊富なREST API とAWS SDKs を提供しています。

## ハンズオンのURL
https://catalog.workshops.aws/amazon-pinpoint-customer-experience/ja-JP/journeys/event-based-journey

## Amazon Pinpointのカスタムイベントを記録

`AWS Pthon SDK Boto3`と`AWS Lambda`を使用して、コードをホストして実行します。

まずは`Lambda`から始めます。`関数を作成`していきましょう。

![](/images/aws-pinpoint-handson-09/2023-08-17-21-29-19.png)

`関数名`、`ランタイム`などを設定していきます。
設定が完了したら、`関数の作成`ボタンをクリックします。

![](/images/aws-pinpoint-handson-09/2023-08-17-21-31-00.png)


関数が作成できたら、下記のコードをコピーして中身を貼り付けます。

```python
import boto3
import datetime
import time

client = boto3.client('pinpoint')

def lambda_handler(event, context):

    application_id = event['application_id']
    endpoint_id = event['endpoint_id']
    event_type = event['event_type']

    response = client.put_events(
            ApplicationId = application_id,
            EventsRequest={
                'BatchItem': {
                    endpoint_id: {
                        'Endpoint': {
                        },
                        'Events':{
                            'registration_success': {
                                'EventType': event_type,
                                'Timestamp': datetime.datetime.fromtimestamp(time.time()).isoformat()
                            }
                        }
                    }
                }
            }
        )

    return response
```

![](/images/aws-pinpoint-handson-09/2023-08-17-21-33-50.png)

次にこの`Lambda 関数`に対して、`Amazon Pinpoint プロジェクト`へ`put_events`を実行できる権限を与えます。

ロール名リンクから、インラインポリシーを作成していきましょう。

![](/images/aws-pinpoint-handson-09/2023-08-17-21-35-06.png)


![](/images/aws-pinpoint-handson-09/2023-08-17-21-37-04.png)

前にも似たようなことをやっているので、ちょっと端折っていますが、下記のJSONを貼り付けて、リージョンとアカウントIDは自分のものに変更していきます。

```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PutEvent",
			"Effect": "Allow",
			"Action": [
				"mobiletargeting:PutEvent*"
			 ],
			"Resource": "arn:aws:mobiletargeting:AWS-REGION:AWS-ACCOUNT-ID:*"
		}
		]
}
```



![](/images/aws-pinpoint-handson-09/2023-08-17-21-42-29.png)

これで、ポリシーの作成ができました。

![](/images/aws-pinpoint-handson-09/2023-08-17-21-44-01.png)


`Lambda 関数`の方に戻ります。

下記のデータを`イベント JSON`に貼り付けます。
※application_idは`Pinpoint`のプロジェクトIDに置き換えます。
※endpoint_idはダイナミックセグメント`older_than_35`をエクスポートし、1列目のIdの値で置き換えてください。

```
{
  "application_id": "---",
  "endpoint_id": "---",
  "event_type": "registration_success"
}
```

ここまでの作成が完了したら、`テスト`を実施します。
下記のように返却されたらOK！！

![](/images/aws-pinpoint-handson-09/2023-08-17-21-51-21.png)


次は`ジャーニー`に移動します。
アクティブな項目にチェックを入れ、`アクション > ジャーニーを複製`を選択します。

複製したら、`アクティビティの実行時に参加者の追加`を選択し、イベント名を`registration_success`と入力し、`保存`ボタンをクリックします。


![](/images/aws-pinpoint-handson-09/2023-08-17-21-55-37.png)

![](/images/aws-pinpoint-handson-09/2023-08-17-21-53-33.png)

`アクション > 設定`に移動し、`開始日時`、`終了日時`の両方で、`リセット`をクリックします。
あとは、下記のスクリーンショット通りの設定を行い、`保存`ボタンをクリックします。

![](/images/aws-pinpoint-handson-09/2023-08-17-21-59-32.png)

![](/images/aws-pinpoint-handson-09/2023-08-17-22-00-29.png)

設定はこれで完了で、`パブリッシュ`します。

最後に`Lambda 関数`からテストを行ってみます。
先ほど作成したイベントベースのジャーニーのテスト英露オードで指定した縁遠いんとを対象に`registration_success`イベントがトリガーされるはずです。

ジャーニーが始まったので、テストしてみます。

![](/images/aws-pinpoint-handson-09/2023-08-17-22-06-12.png)


あれー、、送信できなかった？

![](/images/aws-pinpoint-handson-09/2023-08-17-22-10-00.png)

うーん、まだなんでメールが送信できなかったか分からずじまいでしたが、ひとまず先に進むことにします。
さて、次回ですが、いよいよ分析に入ります。
`ネイティブチャート`のモニタリングをしていきたいと思います。
それではまた次回！
