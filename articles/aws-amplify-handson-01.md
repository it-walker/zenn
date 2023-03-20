---
title: "AWS Amplifyのハンズオンをやってみた（1）"
emoji: "😊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Handson"]
published: true
---

## はじめに
Amplifyに興味が出てきたので、下記のハンズオン資料をもとにとりあえず手を動かしてみようということで、実際にハンズオンを自分でやってみた記録を残すことにしました。
（下記リンクの`02 AWS Amplify のハンズオン（環境構築, Cloud9 編）`の動画を見ながら作業しています。）

https://pages.awscloud.com/JAPAN-event-OE-Hands-on-for-Beginners-amplify-2022-confirmation-774.html

では、さっそく行ってみましょう！

## AWS Cloud9 の環境構築

まずは、環境構築です。AWSコンソールから`Cloud9`にアクセスします。
![](/images/aws-amplify-handson-01/2023-03-18-15-56-16.png)

`Create environment`ボタンをクリックします。
![](/images/aws-amplify-handson-01/2023-03-18-15-58-24.png)

`Name`、`Description`に任意の内容を入力します。
![](/images/aws-amplify-handson-01/2023-03-18-16-02-08.png)

`t2.micro`だとメモリ不足になる可能性があるとのことで、`t3.small`を選択します。
![](/images/aws-amplify-handson-01/2023-03-18-16-09-30.png)

あとはデフォルトの設定そのままで`Create`ボタンをクリックします。
![](/images/aws-amplify-handson-01/2023-03-18-16-03-04.png)

環境構築中となりました。しばらく待ちます。
![](/images/aws-amplify-handson-01/2023-03-18-16-12-52.png)

`Successfully created {Name}`というメッセージが通知されました。
![](/images/aws-amplify-handson-01/2023-03-18-16-14-16.png)

ここまでで環境構築は完了です。

## 初期設定

次に、AWSが管理している一時的な認証情報の設定を無効化します。

`Cloud9`の画面左上にあるメニュー`AWS Cloud9 > Preferences`を選択します。
![](/images/aws-amplify-handson-01/2023-03-18-16-15-12.png)

`AWS SETTINGS`を選択します。
![](/images/aws-amplify-handson-01/2023-03-18-16-22-36.png)

`AWS Resouces`の`Credentials`にある`AWS managed temporary credentials`を OFF にします。
![](/images/aws-amplify-handson-01/2023-03-18-16-25-00.png)

これで設定は完了です。

## EBS ボリュームを引き上げる

デフォルトのままでは、EBS ボリュームが不足してしまう可能性があるので、EBS ボリュームの引き上げを行います。
メニュー`AWS Cloud9 > Go To Your Dashboard`を選択します。

![](/images/aws-amplify-handson-01/2023-03-18-16-26-41.png)

`Name`を選択して詳細画面に遷移します。
![](/images/aws-amplify-handson-01/2023-03-18-16-30-26.png)

EC2 インスタンスを編集したいので、`Manage EC2 instance`ボタンをクリックします。
![](/images/aws-amplify-handson-01/2023-03-18-16-31-04.png)

一度 EC2 インスタンスを停止させます。
![](/images/aws-amplify-handson-01/2023-03-18-16-35-18.png)

`インスタンスの状態 > インスタンスを停止`を選択します。
![](/images/aws-amplify-handson-01/2023-03-18-16-35-36.png)

インスタンスを停止してよいかどうかを聞かれるので、`停止`ボタンをクリックします。
![](/images/aws-amplify-handson-01/2023-03-18-16-36-53.png)

EC2 インスタンスが停止できました。
![](/images/aws-amplify-handson-01/2023-03-18-16-37-48.png)

ここで、マウントされているストレージを確認してみましょう。
`ストレージ`タブを選択し、対象のストレージを選択します。
![](/images/aws-amplify-handson-01/2023-03-18-16-38-51.png)

ボリュームの画面に遷移するので、対象のボリュームを選択し、ボリュームのサイズを変更していきます。
![](/images/aws-amplify-handson-01/2023-03-18-16-40-52.png)

対象のボリュームを選択したら、`アクション > ボリュームの変更`をクリックします。
![](/images/aws-amplify-handson-01/2023-03-18-16-41-17.png)

![](/images/aws-amplify-handson-01/2023-03-18-16-42-17.png)
10GB → 32GB に変更し、`変更`ボタンをクリックします。
![](/images/aws-amplify-handson-01/2023-03-18-16-42-48.png)

確認ダイアログが表示されるので、`変更`ボタンをクリックします。
![](/images/aws-amplify-handson-01/2023-03-18-16-43-41.png)

EC2 ダッシュボードに戻って、EC2インスタンスを再起動します。
`インスタンスの状態 > インスタンスを再起動`をクリックします。

![](/images/aws-amplify-handson-01/2023-03-18-16-45-54.png)

確認ダイアログが表示されるので`再起動`ボタンをクリックします。
![](/images/aws-amplify-handson-01/2023-03-18-16-46-36.png)

EBS ボリュームの引き上げが完了したので、ターミナルから、ボリュームが引き上げられたことを確認していきます。
`Cloud9 IDE`を開きます。
![](/images/aws-amplify-handson-01/2023-03-18-16-48-30.png)

ターミナルから下記のコマンドを実行します。

```
df -h
```

![](/images/aws-amplify-handson-01/2023-03-18-16-52-07.png)

32GB に変更されていることが確認できました！
