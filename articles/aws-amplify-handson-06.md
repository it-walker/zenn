---
title: "AWS Amplify ハンズオンをやってみた（6）"
emoji: "🎉"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Handson"]
published: true
---

## はじめに
この記事は、`AWS Amplify ハンズオンをやってみた（5）`のつづきです。
下記リンクの`07 本シリーズのまとめ、リソースの削除`の動画を見ながら作業しています。

https://pages.awscloud.com/JAPAN-event-OE-Hands-on-for-Beginners-amplify-2022-confirmation-774.html


## リソースの削除

アプリケーションのルートディレクトリに移動してリソースの削除を行なっていきます。
下記コマンドを実行します。

```
amplify delete
```

本当に削除していいですかと聞かれるので、`y`を選択します。

```
$ amplify delete
? Are you sure you want to continue? This CANNOT be undone. (This will delete all the environments of the project from the cloud and wipe out all the local files created by Amplify CLI) (y/N) ‣ 
```

```
$ amplify delete
✔ Are you sure you want to continue? This CANNOT be undone. (This will delete all the environments of the project from the cloud and wipe out all the local files created by Amplify CLI) (y/N) · yes
⠋ Deleting resources from the cloud. This will take a few minutes.
Deleting env: dev.
✔ Project deleted in the cloud.
✅ Project deleted locally.
```

実際に削除できているかどうかを確認していきます。
publish したURLにアクセスしても何も表示されていないことを確認。

![](/images/aws-amplify-handson-06/2023-03-19-22-19-32.png)

`AppSync`にアクセスしてリソースが削除されていることを確認。

![](/images/aws-amplify-handson-06/2023-03-19-22-19-15.png)

`DynamoDB`にアクセスしてリソースが削除されていることを確認。

![](/images/aws-amplify-handson-06/2023-03-19-22-21-17.png)

![](/images/aws-amplify-handson-06/2023-03-19-22-21-44.png)


`Cognito`にアクセスしてリソースが削除されていることを確認。

![](/images/aws-amplify-handson-06/2023-03-19-22-22-28.png)

次に`Cloud9`の環境を削除していきます。
`Cloud9`にアクセスして、

![](/images/aws-amplify-handson-06/2023-03-19-22-23-15.png)

![](/images/aws-amplify-handson-06/2023-03-19-22-23-30.png)

![](/images/aws-amplify-handson-06/2023-03-19-22-25-29.png)

## 最後に
はい、これで全ての作業が完了できました。
初めてやったので多少戸惑いはあったものの、最後までやり切ることができました。
今後もっと色々と触ってみて知見を増やしていきたいです。