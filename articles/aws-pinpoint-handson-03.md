---
title: "Amazon Pinpointのハンズオンをやってみた（その３）"
emoji: "🙌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Pinpoint", "Handson"]
published: true
---

## はじめに

Amazon Pinpointのハンズオンの３回目をお送りします。
Lambda Functionで、エンドポイントの作成をやっていきたいと思います。

## ハンズオンのURL
https://catalog.workshops.aws/amazon-pinpoint-customer-experience/ja-JP/prerequisites/create-a-project


## AWS Lambda Function の作成と実行
ではでは、行ってみますか。
`Lambda`へ移動します。
移動したら、`関数の作成`ボタンをクリックします。


![](/images/aws-pinpoint-handson-03/2023-08-12-14-57-26.png)


![](/images/aws-pinpoint-handson-03/2023-08-12-14-59-17.png)

`一から作成`を選択し、任意の関数名をつけ、ランタイムには`Python3.11`を選択し、`関数の作成`ボタンをクリックしていきます。
（ハンズオンでは`Phthon3.9`だったけど、最新のものを使っちゃう）


![](/images/aws-pinpoint-handson-03/2023-08-12-15-01-49.png)

はい、というわけで、ここまであっという間にできてしまいました。

![](/images/aws-pinpoint-handson-03/2023-08-12-15-03-08.png)

## 関数の中身を実装
以下のコードをコピーし、`lambda_function`に貼り付けてください。

```
import boto3

client = boto3.client('pinpoint')

def lambda_handler(event, context):

	application_id = event['application_id']
	first_name = event['first_name']
	email_address = event['email_address']
	endpoint_id = event['endpoint_id']
	user_id = event['user_id']
	age = event['age']
	interests = event['interests']

	response = client.update_endpoint(
	ApplicationId=application_id,
	EndpointId= endpoint_id,
	EndpointRequest={
		'Address': email_address,
		'ChannelType': 'EMAIL',
		'Metrics': {
			'age': age
		},
		'OptOut': 'NONE',
		'User': {
			'UserAttributes': {
				'FirstName': [
					first_name,
				],
				'interests': [
					interests
				]
			},
			'UserId': user_id
		}
	}
	)

	return response
```

## 権限の付与
Amazon Pinpointのプロジェクトに対して`AWS Lambda Function`が`update_endpoint`操作を実行できるようにする必要があるため、IAMポリシーを追加していきます。

`設定 > アクセス権限`に移動し、`ロール名`のリンクをクリックします。

![](/images/aws-pinpoint-handson-03/2023-08-12-15-07-44.png)

`許可の追加 > インラインポリシーを作成`を選択します。

![](/images/aws-pinpoint-handson-03/2023-08-12-15-10-39.png)


アクセス許可を指定する画面に遷移しましたので、ここで、`JSON`タブに切り替えます。

![](/images/aws-pinpoint-handson-03/2023-08-12-15-11-42.png)

以下のJSONに差し替えます。

```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "UpdateEndpoint",
			"Effect": "Allow",
			"Action": [
				"mobiletargeting:UpdateEndpoint*"
			 ],
			"Resource": "arn:aws:mobiletargeting:AWS-REGION:AWS-ACCOUNT-ID:*"
		}
		]
}
```

`AWS-REGION`は自身の使用リージョン、`AWS-ACCOUNT-ID`は自分のアカウントIDに置き換えてください。
下記のコマンドで、アカウントIDを確認することができるよ。

```
aws sts get-caller-identity
```

これで、許可ポリシーの設定が完了しました。
次はまた、Lambdaに戻るよー

## テストの作成

![](/images/aws-pinpoint-handson-03/2023-08-12-15-20-27.png)

`コード`にある`Test`ボタンのドロップダウンを選択し、`Configure test event`を選択します。

![](/images/aws-pinpoint-handson-03/2023-08-12-15-21-43.png)

![](/images/aws-pinpoint-handson-03/2023-08-12-15-23-11.png)

`イベント名`に`test`と入力します（ここはなんでもいい）。
`イベントJSON`のところを、下記のコードに置き換えます。
※`application_id`はPinpointのプロジェクトIDに置き換えます
※`email_address`は登録したメールアドレスに置き換えます

```
{
    "application_id" : "---",
    "first_name" : "Jake",
    "email_address" : "---",
    "endpoint_id" : "222",
    "user_id" : "userid2",
	"age": 35,
	"interests": "shirts"
}
```

ここまでできたら、`保存`ボタンをクリックします。

![](/images/aws-pinpoint-handson-03/2023-08-12-15-27-52.png)

次に`Deploy`ボタンをクリックします。

![](/images/aws-pinpoint-handson-03/2023-08-12-15-28-44.png)

これでテストの準備が整ったので、早速テストしてみましょう。
`テスト`ボタンをクリックします。

```
"An error occurred (AccessDeniedException) when calling the UpdateEndpoint operation: ...
```

あれっ、何か設定間違えたか！？
設定を確認してみます。
・・・しまった、インラインポリシーがちゃんと追加できていなかった。
権限がないので、エラーになっていたみたいです。


気を取り直して再度テストを実行します。
下記のような感じで、うまく成功したみたいです。

![](/images/aws-pinpoint-handson-03/2023-08-12-15-44-05.png)

というわけで、Lambda Functionからエンドポイントの作成を行ってみました。
次回は、`S3イベント通知を使用そたエンドポイントの自動インポート`をやってみます。
それでは、また！
