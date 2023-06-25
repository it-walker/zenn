---
title: "[AWS Hands-on for Beginners]Serverlessのハンズオンを実際にやってみたよ（2）"
emoji: "📑"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Lambda", "Translate"]
published: true
---

## AWS Lambda ハンズオン② 他のサービスを呼び出してみる

前回は純粋にLambdaを使ってみただけだったので、今回は他のサービス（AWS SDKの翻訳サービス）を呼び出してみるようです。

リンクは下記。

[AWS SDK for Python (Boto3)](https://aws.amazon.com/jp/sdk-for-python/)

[APIリファレンス](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/index.html)

[Translate](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/translate.html)

## 実装

```
import json
import boto3

translate = boto3.client('translate')

def lambda_handler(event, context):

  input_text = 'おはよう'

  response = translate.translate_text(
      Text=input_text,
      SourceLanguageCode='ja',
      TargetLanguageCode='en',
      Settings={
          'Formality': 'FORMAL'|'INFORMAL',
          'Profanity': 'MASK'
      }
  )

  output_text = response.get('TranslatedText')

  return {
    'statusCode': 200,
    'body': json.dumps({
        'output_text': output_text
    })
  }
```

## ロールを修正
このままだと権限がないので実行できません。
ということで、ロールの権限を修正していきましょう。

![](/images/aws-serverless-handson-02/2023-06-25-13-20-39.png)

動画だとすぐ見つかる場所にありそうだったのですが、今現在は設定の中に入ってしまっているようで若干見つけるのに苦戦しました。。

ロールを表示して、権限をみていきます。
`許可を追加`の`ポリシーをアタッチ`を選択します。

![](/images/aws-serverless-handson-02/2023-06-25-13-26-11.png)

`Translate`と入力して、候補を絞ります。

![](/images/aws-serverless-handson-02/2023-06-25-13-27-38.png)

今回は、ハンズオンなので、`TranslateFullAccess`を選択して、`許可を追加`ボタンをクリックします。

![](/images/aws-serverless-handson-02/2023-06-25-13-28-32.png)

これで権限の追加が完了しました。

![](/images/aws-serverless-handson-02/2023-06-25-13-30-14.png)


ハンズオン動画だと、レイヤーに`Translate`が追加されているのですが、今だと表示されないですね・・

![](/images/aws-serverless-handson-02/2023-06-25-13-31-48.png)

それでは、テストを実行してみましょう。
（テストを実行する前に`Deploy`が必要みたいです。`Deploy`ボタンをクリックしておいてください。）

![](/images/aws-serverless-handson-02/2023-06-25-13-33-27.png)

エラーになってる・・

![](/images/aws-serverless-handson-02/2023-06-25-13-34-59.png)

どうも、`Translate`の`Settings`がいらないようですね。。
余計な記述をいったん削除してみました。

```
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
    })
  }
```

これで再度実行してみます。

![](/images/aws-serverless-handson-02/2023-06-25-13-44-47.png)

うん、まぁできたはできた。
ただ、ついでに入れておいたインプットの日本語が文字化けしとるやん。

ついでにもう少し首を突っ込んでみたいと思います。
せっかくなので、インプットの文字列も文字コードではなく文字として表示したい。

下の記事が参考になりそう。

https://tex2e.github.io/blog/python/json-dumps-ensure-ascii-false


というわけで、`ensure_ascii=False`を入れてみることにしますよ。

```
  return {
    'statusCode': 200,
    'body': json.dumps({
      'input_text': input_text,
      'output_text': output_text
    }, ensure_ascii=False)
  }
```

お、できた！！

![](/images/aws-serverless-handson-02/2023-06-25-13-51-10.png)

## さいごに
ライブラリとして、すでに用意してあるものを利用する分には、かんたんに実装できてしまうのですねー！
驚きです。。
