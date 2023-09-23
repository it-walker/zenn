---
title: "Amazon Pinpointのハンズオンをやってみた（その８）"
emoji: "😺"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Pinpoint", "Handson"]
published: true
---

## はじめに

Amazon Pinpointのハンズオン８回目をお送りします。
`ジャーニーの作成`をやっていきたいと思います。

## ジャーニーとは
> ジャーニーとは、カスタマイズされた複数ステップのカスタマーエンゲージメントを実現する機能です。ジャーニーを作成するには、セグメントまたはカスタムイベントを使い、どのカスタマーがジャーニーに参加するかを定義します。次に、カスタマーがジャーニーで辿るアクティビティを設定します。アクティビティには、メッセージの送信や、カスタマーのアクションによる分岐などがあります。
> ジャーニーの詳細については、[こちら](https://docs.aws.amazon.com/pinpoint/latest/userguide/journeys.html) を参照してください。

## ハンズオンのURL
https://catalog.workshops.aws/amazon-pinpoint-customer-experience/ja-JP/journeys/creating-a-journey

## Eメールのキャンペーン設定

35歳より上の顧客に対し、`ウェルカムメール`を送信するシンプルなジャーニーを構築します。

`ジャーニー`を選択し、`ジャーニーを作成`をクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-19-58-09.png)

任意のタイトルを入力します。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-04-03.png)

`ジャーニーにようこそ`の`次へ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-05-53.png)


`すべてのジャーニーには始まりがある`も`次へ`ボタンをクリックする。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-07-21.png)

`マルチチャネルのジャーニーを作成`も`次へ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-09-49.png)

`ジャーニーを構築`も`次へ`ボタンをクリックする。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-08-35.png)

`ジャーニーの名前とステータス`が出てきました。これも`次へ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-11-38.png)

`ジャーニーのスケジュール`が出てきました。これも`次へ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-12-55.png)


`ジャーニーのアクティビティを編集`も`次へ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-15-21.png)

`画面の制御`も同様に`次へ`ボタンをクリックします。


![](/images/aws-pinpoint-handson-08/2023-08-17-20-13-49.png)

`ジャーニーのテストとパブリッシュ`も`次へ`ボタンをクリックします。


![](/images/aws-pinpoint-handson-08/2023-08-17-20-16-31.png)


`フィードバックボタン`は`ご利用開始`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-17-44.png)

`ジャーニーのエントリ`が使えるようになりました。
`エントリ条件を設定`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-19-28.png)

`セグメント`に`other_than_35`を選択し、`Rate`は`しない`、`説明`は適当に意味のわかる説明を入力したら、`保存`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-21-36.png)


これでエントリ条件の設定が保存されました。
次は、`Add activity`をクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-25-23.png)

`Add activity`から新しいジャーニーのブロックとして`Eメールを送信`を追加します。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-29-15.png)


メールテンプレートは以前作成したテンプレートが選択できるので、それを選択します。入力し終えたら`保存`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-30-22.png)

次は、`はい/いいえ分割`を選択します。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-32-38.png)

`条件タイプ`、条件などを下記のように設定し、`保存`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-34-25.png)


`No`の分岐のところの`Add activity`をクリックして、先ほどと同じ`Eメールを送信`のブロックを追加します。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-35-38.png)

設定が完了したら、`保存`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-37-23.png)


これでジャーニーの設定は完了です。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-39-50.png)

![](/images/aws-pinpoint-handson-08/2023-08-17-20-40-03.png)

最後に`ジャーニーの公開`を行います。`アクション > 設定`に移動します。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-40-54.png)

`ジャーニーの開始日と終了日`を設定して、`保存`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-43-06.png)

公開する前に、`レビュー`します。
`レビュー`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-44-28.png)


これでOKかと思いきや、設定エラーですって。
そうか、開始時間を未来日時にしないといけないのね。

というわけで、1日後に開始するようにしておきます。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-46-41.png)

![](/images/aws-pinpoint-handson-08/2023-08-17-20-45-40.png)

エラーがなくなりました。今度こそOKなのか！？

![](/images/aws-pinpoint-handson-08/2023-08-17-20-47-19.png)

もう少しあるみたい。


![](/images/aws-pinpoint-handson-08/2023-08-17-20-48-12.png)

`レビュー済みとしてマーク`をクリックします。
これで、完了なので`パブリッシュ`ボタンをクリックします。

![](/images/aws-pinpoint-handson-08/2023-08-17-20-55-04.png)

これでパブリッシュされました！！

![](/images/aws-pinpoint-handson-08/2023-08-17-20-57-21.png)


なかなか長かったですが、これでジャーニーの作成が完了しました。
今回はここまでで、次回は、`イベントベースのジャーニー`をやってみます。
どうやらこれはオプションらしいので、やってもらやなくてもいい！？のかもしれないけど、まぁチャレンジしていきましょうかねー。
