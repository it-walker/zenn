---
title: "SNSログイン機能を実装してみた（２）"
emoji: "💬"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Login", "SNS"]
published: true
---

## はじめに

前回、「SNS ログイン機能を実装してみた（１）」では、SNS ログイン機能の実装に挑戦しました。
しかし、これが失敗に終わったため、再チャレンジです。

## とりあえず、Amplify Studio を眺めてみる

まずは原因を探るべく、`Amplify Studio`を覗いてみることにしました。
`Amplify Studio > Authentication`の状態を見てみます。

![](/images/20230914-amplify-sns-login-02/2023-09-16-22-14-36.png)

おろ！？`Add login mechanism`という設定があるぞ。
ドロップダウンをクリックしてみると、SNS の設定項目が。。
ひょっとしてこれなんじゃ！？

![](/images/20230914-amplify-sns-login-02/2023-09-16-22-16-14.png)

とりあえず、`Google`を選択してみましょうか。
あ、項目増えましたね。
`Web Client ID`、`Web Client Secret`ってなんだ？

![](/images/20230914-amplify-sns-login-02/2023-09-16-22-17-42.png)

あ！認証情報作ったときに出てきたなー。
あれって、控えとかなきゃいけないやつ〜〜？
->`Web Client ID`は表示されているけど、`Web Client Secret`が見当たらないや

仕方ないので、もう一度認証情報を作り直してみます。

![](/images/20230914-amplify-sns-login-02/2023-09-16-22-22-58.png)

あ、やっぱりあったや。
（JSON をダウンロードしとこう・・）

ローカルの URL と、デプロイ環境の URL を追加しておきます。

![](/images/20230914-amplify-sns-login-02/2023-09-16-22-25-19.png)

`deploy`ボタンをクリックします。

![](/images/20230914-amplify-sns-login-02/2023-09-16-22-34-50.png)

![](/images/20230914-amplify-sns-login-02/2023-09-16-22-35-03.png)

deploy 完了したみたいです。
書いてある指示通りに実行してみますか。

![](/images/20230914-amplify-sns-login-02/2023-09-16-22-38-37.png)

amplify の設定を取得するのに、`amplify pull`コマンドを実行していきます。

```
amplify pull --appId <appId> --envName <envName>
```

環境が整ったはずなので、ローカルで実行してみましょう。

```
npm start
```

おっ！、項目自体は出てきました！！！

![](/images/20230914-amplify-sns-login-02/2023-09-16-22-41-57.png)

これでできたっしょ！と思ったのですが・・

![](/images/20230914-amplify-sns-login-02/2023-09-16-22-45-03.png)

うーむ、、何か設定を間違えたのだろうか・・
