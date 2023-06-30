---
title: "[AWS Hands-on for Beginners]Serverlessのハンズオンを実際にやってみたよ（6）"
emoji: "😺"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "API", "Gateway", "DinamoDB"]
published: true
---

## Amazon DynamoDB ハンズオン② API Gateway と Lambda と DynamoDB を組み合わせる

それでは、このハンズオンシリーズの最後になります。
これまで作成してきた`API Gateway`、`Lambda`、`DynamoDB`を組み合わせていきます。



まずは、ソースコードの修正を行います。
下記を参考に、修正していきます。

https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/dynamodb/table/index.html


```diff
import json
import boto3
+import datetime

translate = boto3.client('translate')

+dynamodb_translate_history_table = boto3.resource('dynamodb').Table('translate-history')

def lambda_handler(event, context):

  input_text = event['queryStringParameters']['input_text']

  response = translate.translate_text(
    Text=input_text,
    SourceLanguageCode='ja',
      TargetLanguageCode='en',
  )

  output_text = response.get('TranslatedText')

+  dynamodb_translate_history_table.put_item(
+    Item = {
+      'timestamp': datetime.datetime.now().strftime("%Y%m%d%H%M%S"),
+      'input_text': input_text,
+      'output_text': output_text
+    }
+  )

  return {
    'statusCode': 200,
    'body': json.dumps({
      'input_text': input_text,
      'output_text': output_text
    }, ensure_ascii=False),
    'isBase64Encoded': False,
    'headers': {}
  }
```

次に、DynamoDBが使えるように、ロールの設定を行っていきます。
下記のURLをクリックしてください。


![](/images/aws-serverless-handson-06/2023-06-30-20-03-34.png)

ポリシーをアタッチしていきます。


![](/images/aws-serverless-handson-06/2023-06-30-20-05-18.png)

`dynamo`と入力していくと候補が絞られます。
`AmazonDynamoDBFullAccess`を追加していきましょう。

![](/images/aws-serverless-handson-06/2023-06-30-20-06-27.png)

![](/images/aws-serverless-handson-06/2023-06-30-20-07-15.png)

それでは、テストしてみましょう。

![](/images/aws-serverless-handson-06/2023-06-30-20-08-44.png)


![](/images/aws-serverless-handson-06/2023-06-30-20-09-17.png)

さあ、テストが実施できたので、DynamoDBに登録されているか確認してみましょう。

![](/images/aws-serverless-handson-06/2023-06-30-20-09-39.png)

おおっ、できました。

では、最後に、実際にAPIを叩いてみましょうか。
`API Gateway`からURLをクリックしましょう。

![](/images/aws-serverless-handson-06/2023-06-30-20-15-30.png)

DynamoDBの方にも、登録されていることを確認することができました。

![](/images/aws-serverless-handson-06/2023-06-30-20-16-28.png)


![](/images/aws-serverless-handson-06/2023-06-30-20-13-33.png)

## さいごに
まずは手を動かしてみようということで、ハンズオンの通りにやってみました。
いかがだったでしょうか。
バージョンが若干更新されているので、少し戸惑いましたが、おおむね指示通りで最後まで辿り着くことができました！

さあ、最後に後片付けしちゃいましょう。
