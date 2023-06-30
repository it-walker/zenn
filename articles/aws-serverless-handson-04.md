---
title: "[AWS Hands-on for Beginners]Serverlessのハンズオンを実際にやってみたよ（4）"
emoji: "🕌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "API", "Gateway"]
published: true
---

## Amazon API Gateway ハンズオン② API Gateway と Lambda を組み合わせる

それでは、続きをやっていきましょう。
今回は、新たに`リソース`を作っていきます。
`アクション>リソースの作成`をクリックします。

![](/images/aws-serverless-handson-04/2023-06-25-20-58-29.png)

`リソース名`に名前を入力します。
今回は`translate`と入力しています。

![](/images/aws-serverless-handson-04/2023-06-25-20-59-50.png)

次に、`メソッド`を作成します。
`アクション>メソッドの作成`をクリックします。

![](/images/aws-serverless-handson-04/2023-06-25-21-00-19.png)

メソッドが作成されると、`/translate`が表示されているので、`GET`を選択します。

![](/images/aws-serverless-handson-04/2023-06-25-21-00-42.png)

`GETのセットアップ`を行います。

![](/images/aws-serverless-handson-04/2023-06-25-21-01-04.png)

`統合タイプ`については、そのまま`Lambda 関数`を選択します。
それ以外の設定はそのままで、`Lambda 関数`については、前に作成した`translateFunction`を入力します。


![](/images/aws-serverless-handson-04/2023-06-25-21-02-03.png)

`Lambda 関数に権限を追加する`画面が表示されますが、そのまま`OKボタン`をクリックします。

![](/images/aws-serverless-handson-04/2023-06-25-21-02-21.png)

`GET メソッドの実行`画面が表示されます。

![](/images/aws-serverless-handson-04/2023-06-25-21-03-10.png)

`メソッドリクエスト`をクリックします。

![](/images/aws-serverless-handson-04/2023-06-25-21-03-52.png)

`URL クエリ文字列パラメータ`を展開して、`クエリ文字列の追加`のリンクをクリックします。

![](/images/aws-serverless-handson-04/2023-06-25-21-04-11.png)

![](/images/aws-serverless-handson-04/2023-06-25-21-04-33.png)


リクエストパラメータとして、`input_text`と入力します。

![](/images/aws-serverless-handson-04/2023-06-25-21-04-57.png)

次に`テスト`のためにソースコードを少し修正します。
`テスト`をクリックします。

![](/images/aws-serverless-handson-04/2023-06-25-21-05-29.png)


![](/images/aws-serverless-handson-04/2023-06-25-21-06-02.png)

![](/images/aws-serverless-handson-04/2023-06-25-21-06-27.png)

レスポンスを調整する必要があるため、下記のように修正します。

```diff
import json
import boto3

translate = boto3.client('translate')

def lambda_handler(event, context):

  input_text = 'おはよう'

  response = translate.translate_text(
    Text=input_text,
    SourceLanguageCode='ja',
    TargetLanguageCode='en',
  )

  output_text = response.get('TranslatedText')

  return {
    'statusCode': 200,
    'body': json.dumps({
      'input_text': input_text,
      'output_text': output_text
    }, ensure_ascii=False),
+    'isBase64Encoded': False,
+    'headers': {}
  }
```

次にテストの設定を行います。
`Test>Configure test event`をクリックします。

![](/images/aws-serverless-handson-04/2023-06-25-21-09-49.png)

すでにあるテストイベントの設定を編集します。
元々`保存されたイベントを編集`が選択されていますが、`新しいイベントを作成`を選択します。

![](/images/aws-serverless-handson-04/2023-06-25-21-10-12.png)

`テンプレート - オプション`から`api`と入力すると、`API Gateway AWS Proxy`を選択します。

![](/images/aws-serverless-handson-04/2023-06-25-21-10-51.png)

`API Gateway Proxy`のテンプレートは下記になります。（思ってたより長かった・・）

```
{
  "body": "eyJ0ZXN0IjoiYm9keSJ9",
  "resource": "/{proxy+}",
  "path": "/path/to/resource",
  "httpMethod": "POST",
  "isBase64Encoded": true,
  "queryStringParameters": {
    "foo": "bar"
  },
  "multiValueQueryStringParameters": {
    "foo": [
      "bar"
    ]
  },
  "pathParameters": {
    "proxy": "/path/to/resource"
  },
  "stageVariables": {
    "baz": "qux"
  },
  "headers": {
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8",
    "Accept-Encoding": "gzip, deflate, sdch",
    "Accept-Language": "en-US,en;q=0.8",
    "Cache-Control": "max-age=0",
    "CloudFront-Forwarded-Proto": "https",
    "CloudFront-Is-Desktop-Viewer": "true",
    "CloudFront-Is-Mobile-Viewer": "false",
    "CloudFront-Is-SmartTV-Viewer": "false",
    "CloudFront-Is-Tablet-Viewer": "false",
    "CloudFront-Viewer-Country": "US",
    "Host": "1234567890.execute-api.us-east-1.amazonaws.com",
    "Upgrade-Insecure-Requests": "1",
    "User-Agent": "Custom User Agent String",
    "Via": "1.1 08f323deadbeefa7af34d5feb414ce27.cloudfront.net (CloudFront)",
    "X-Amz-Cf-Id": "cDehVQoZnx43VYQb9j2-nvCh-9z396Uhbp027Y2JvkCPNLmGJHqlaA==",
    "X-Forwarded-For": "127.0.0.1, 127.0.0.2",
    "X-Forwarded-Port": "443",
    "X-Forwarded-Proto": "https"
  },
  "multiValueHeaders": {
    "Accept": [
      "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8"
    ],
    "Accept-Encoding": [
      "gzip, deflate, sdch"
    ],
    "Accept-Language": [
      "en-US,en;q=0.8"
    ],
    "Cache-Control": [
      "max-age=0"
    ],
    "CloudFront-Forwarded-Proto": [
      "https"
    ],
    "CloudFront-Is-Desktop-Viewer": [
      "true"
    ],
    "CloudFront-Is-Mobile-Viewer": [
      "false"
    ],
    "CloudFront-Is-SmartTV-Viewer": [
      "false"
    ],
    "CloudFront-Is-Tablet-Viewer": [
      "false"
    ],
    "CloudFront-Viewer-Country": [
      "US"
    ],
    "Host": [
      "0123456789.execute-api.us-east-1.amazonaws.com"
    ],
    "Upgrade-Insecure-Requests": [
      "1"
    ],
    "User-Agent": [
      "Custom User Agent String"
    ],
    "Via": [
      "1.1 08f323deadbeefa7af34d5feb414ce27.cloudfront.net (CloudFront)"
    ],
    "X-Amz-Cf-Id": [
      "cDehVQoZnx43VYQb9j2-nvCh-9z396Uhbp027Y2JvkCPNLmGJHqlaA=="
    ],
    "X-Forwarded-For": [
      "127.0.0.1, 127.0.0.2"
    ],
    "X-Forwarded-Port": [
      "443"
    ],
    "X-Forwarded-Proto": [
      "https"
    ]
  },
  "requestContext": {
    "accountId": "123456789012",
    "resourceId": "123456",
    "stage": "prod",
    "requestId": "c6af9ac6-7b61-11e6-9a41-93e8deadbeef",
    "requestTime": "09/Apr/2015:12:34:56 +0000",
    "requestTimeEpoch": 1428582896000,
    "identity": {
      "cognitoIdentityPoolId": null,
      "accountId": null,
      "cognitoIdentityId": null,
      "caller": null,
      "accessKey": null,
      "sourceIp": "127.0.0.1",
      "cognitoAuthenticationType": null,
      "cognitoAuthenticationProvider": null,
      "userArn": null,
      "userAgent": "Custom User Agent String",
      "user": null
    },
    "path": "/prod/path/to/resource",
    "resourcePath": "/{proxy+}",
    "httpMethod": "POST",
    "apiId": "1234567890",
    "protocol": "HTTP/1.1"
  }
}
```

今回は、この部分の一部を修正します。

```diff
{
  "body": "eyJ0ZXN0IjoiYm9keSJ9",
  "resource": "/{proxy+}",
  "path": "/path/to/resource",
  "httpMethod": "POST",
  "isBase64Encoded": true,
  "queryStringParameters": {
-    "foo": "bar"
+    "input_text": "こんにちは"
  },
.
.
.
```

あとはテストイベント名を入力すれば、完成です。
`保存`ボタンをクリックします。

![](/images/aws-serverless-handson-04/2023-06-25-21-16-16.png)

関数の中身をもう少し修正します。
クエリパラメータから入力値をもらい、それを変数に格納するようにします。
これでひとまず完成かな。

```diff
def lambda_handler(event, context):

-    input_text = 'おはよう'
+    input_text = event['queryStringParameters']['input_text']
```

テストを実行してみると、一応、ちゃんと返ってきた！

![](/images/aws-serverless-handson-04/2023-06-25-21-44-32.png)

ここまでできたら、最後に`API のデプロイ`を行います。
`アクション>APIPのデプロイ`をクリックします。

![](/images/aws-serverless-handson-04/2023-06-25-21-45-38.png)

`デプロイされるステージ`は`dev`を選択し、`デプロイ`ボタンをクリックします。

![](/images/aws-serverless-handson-04/2023-06-25-21-45-56.png)

画面上部にURLが表示されています。
このURLにアクセスしてみましょう。
うまく行っているかなーー・・

![](/images/aws-serverless-handson-04/2023-06-25-21-46-16.png)

Internal Server Error !?
あ、そうか、パラメータを渡してないからか。

![](/images/aws-serverless-handson-04/2023-06-25-21-46-36.png)

というわけで、クエリパラメータを下記のような感じで入力してみます。

```
https:〜/dev/translate?input_text=おはよう
```

すると、予定通り、ちゃんと変換されて返ってくることが確認できました！！

![](/images/aws-serverless-handson-04/2023-06-25-21-48-36.png)

