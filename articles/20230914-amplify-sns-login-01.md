---
title: "SNSログイン機能を実装してみた（１）"
emoji: "🍣"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Login", "SNS"]
published: true
---

## はじめに

先日、「Amplify のプレビュー機能を有効化してみた話」という記事を投稿したのですが、その中で`Authentication`の機能を追加しました。
本日はその続きで、「やっぱり SNS でログインできないとね」という欲が出てきましたので、SNS ログイン機能を実装してみたいと思います。
Amplify のドキュメントを見るとかんたんにできそう！
というわけで、さっそくドキュメントを眺めつつ実践してみたいと思います。

過去の記事はコチラ！↓
[Amplify でプレビュー機能を有効化してみた話](https://zenn.dev/rinteq/articles/amplify-preview)

## 完成予想

こちら公式ドキュメントからの引用ですが、こんな感じのものを想像しています。
（今回は Google のログインしかやらないけど）

![](/images/20230914-amplify-sns-login-01/2023-09-16-10-41-45.png)

https://ui.docs.amplify.aws/react/connected-components/authenticator/configuration#social-providers

## Google のアカウント作成

で、まず何をやるのか。
Google の開発者コンソールで環境の準備が必要そうですね。
Google 開発者コンソールに移動してみます。

https://console.cloud.google.com/projectselector2/apis/dashboard?supportedpurview=project

`プロジェクトの選択`をクリックします。

![](/images/20230914-amplify-sns-login-01/2023-09-14-23-03-59.png)

`新しいプロジェクト`をクリックします。

![](/images/20230914-amplify-sns-login-01/2023-09-14-23-05-29.png)

プロジェクト名を入力し、`作成`をクリックします。

![](/images/20230914-amplify-sns-login-01/2023-09-14-23-06-51.png)

プロジェクトが作成されたら、左側のナビゲーションメニューから`API とサービス > 認証情報`を選択します。

![](/images/20230914-amplify-sns-login-01/2023-09-14-23-09-42.png)

`同意画面を構成`をクリックします

![](/images/20230914-amplify-sns-login-01/2023-09-15-12-50-25.png)

`作成`をクリックします

![](/images/20230914-amplify-sns-login-01/2023-09-15-12-50-49.png)

`アプリ名`と`ユーザーサポートメール`を入力して、`保存して次へ`ボタンをクリックします。

![](/images/20230914-amplify-sns-login-01/2023-09-15-12-52-05.png)

`保存して次へ`ボタンをクリックします。

![](/images/20230914-amplify-sns-login-01/2023-09-15-12-52-32.png)

`保存して次へ`ボタンをクリックします。

![](/images/20230914-amplify-sns-login-01/2023-09-15-19-45-58.png)

テストユーザーは 1 人必要かなと思い、自分のメールアドレスを 1 件追加しました。
その後、`保存して次へ`ボタンをクリックします。

![](/images/20230914-amplify-sns-login-01/2023-09-15-19-47-28.png)

次に、認証情報を作成しなければならないようです。
`認証情報を作成 > OAuth クライアント ID`を選択します。

![](/images/20230914-amplify-sns-login-01/2023-09-16-09-50-00.png)

`アプリケーションの種類`と`名前`の入力が必要のようで、選択、入力していきます。
その後、`作成`ボタンをクリックします。

![](/images/20230914-amplify-sns-login-01/2023-09-16-09-51-09.png)

これで OAuth クライアント作成の完了です！

![](/images/20230914-amplify-sns-login-01/2023-09-16-09-51-50.png)

次の作業は`amplify add auth`だったのですが、こちらは前回実施済みなのでスキップします。

```
// 前回作成済みなので、今回はスキップ
amplify add auth
```

1 つ設定忘れ。
OAuth クライアントのところで、`承認済みのJavaScript生成元`と`承認済みのリダイレクトURI`を追加します。
ここは、Amplify の URI を設定しました。

![](/images/20230914-amplify-sns-login-01/2023-09-16-10-07-25.png)

画面下に`OAuth クライアントを保存しました`と表示されれば OK！

![](/images/20230914-amplify-sns-login-01/2023-09-16-10-07-55.png)

## フロントエンドのセットアップ

Google の設定が終わったので、実装に入ります。
修正はこれだけでいいみたい。

```diff tsx
export function App({ signOut, user }: WithAuthenticatorProps) {
  return (
    <Flex direction="column" justifyContent="center">
-      <Authenticator>
+      <Authenticator socialProviders={['amazon', 'apple', 'facebook', 'google']}>
        {({ signOut, user }) => (
          <main>
            <div className="App">

              （省略）

            </div>
          </main>
        )}
      </Authenticator>
    </Flex>
  )
}
```

いざ、実行してみましょう。
・
・
・

え！？変わらん・・なぜだ・・

![](/images/20230914-amplify-sns-login-01/2023-09-16-10-37-25.png)

## さいごに

というわけで、今回は失敗に終わってしまいました。
だけど、もう少し粘ってみます。
次回はもう少し原因の調査などを行ってみたいと思います。
