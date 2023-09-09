---
title: "Amplifyでプレビュー機能を有効化してみた話"
emoji: "🙆"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify"]
published: true
---

## はじめに

`Amplifyのプレビュー機能`、ブランチごとに環境を作って動作確認できるなんて・・
業務なんかでは、ステージング環境が少なくて、自分達で自由に扱えなかったなんてことがあったけど、これならいいね！こんな環境が欲しかった！というわけで、このプレビュー機能を堪能するべく、実際にやってみたお話です。

## まずはプレビュー機能の設定
さっそくやってみましょう。
まずは、設定から。

`Amplify`のページにある`アプリの設定 > プレビュー`から、`プレビューを有効化`ボタンをクリックします。

![](/images/amplify-preview/2023-09-09-14-20-10.png)

`Github アプリケーションをインストールしてプレビューを有効化`の画面が表示されるので、`GitHun アプリケーションをインストール`ボタンをクリックします。
すると、Githubの画面に遷移するので、まだ未インストールの人はここで、アプリをインストールしてください。

![](/images/amplify-preview/2023-09-09-14-20-27.png)

`develop`を選択して`管理`ボタンをクリックします。

![](/images/amplify-preview/2023-09-09-14-21-55.png)

`develop ブランチのプレビュー設定を管理`画面にて、`プルリクエストのプレビュー`にチェックを入れ、`プルリクエストのプレビュー - バックエンド環境`は、`すべての ...`にしてみました。
最後に`確認`ボタンをクリックします。

![](/images/amplify-preview/2023-09-09-14-22-35.png)

これで設定は完了です。

![](/images/amplify-preview/2023-09-09-14-23-00.png)

## ちょうどいいからついでに、Authenticatorも。

Amplify環境を最初にこしらえてありまして、これから、認証機能を追加してみたいと思います。
まずはローカルにて認証機能を追加していきます。

```
amplify add auth
Using service: Cognito, provided by: awscloudformation

 The current configured provider is Amazon Cognito.

 Do you want to use the default authentication and security configuration? Def
ault configuration
 Warning: you will not be able to edit these selections.
 How do you want users to be able to sign in? Email or Phone Number
 Do you want to configure advanced settings? No, I am done.
✅ Successfully added auth resource mylibrary8a675d6c locally

✅ Some next steps:
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud

⚠️ You have enabled SMS based auth workflow. Verify your SNS account mode in the SNS console: https://console.aws.amazon.com/sns/v3/home#/mobile/text-messaging
If your account is in "Sandbox" mode, you can only send SMS messages to verified recipient phone numbers.
```

状態を確認してみます。
`Auth`が追加されたことが確認できました。

```
amplify status

    Current Environment: dev

┌──────────┬───────────────────┬───────────┬───────────────────┐
│ Category │ Resource name     │ Operation │ Provider plugin   │
├──────────┼───────────────────┼───────────┼───────────────────┤
│ Auth     │ mylibrary8a675d6c │ Create    │ awscloudformation │
└──────────┴───────────────────┴───────────┴───────────────────┘
```

追加できたので、Amplify環境に取り込むために`amplify push`を実行します。

```
amplify push
⠧ Fetching updates to backend environment: dev from the cloud.⠋ Building resou
✔ Successfully pulled backend environment dev from the cloud.

    Current Environment: dev

┌──────────┬───────────────────┬───────────┬───────────────────┐
│ Category │ Resource name     │ Operation │ Provider plugin   │
├──────────┼───────────────────┼───────────┼───────────────────┤
│ Auth     │ mylibrary8a675d6c │ Create    │ awscloudformation │
└──────────┴───────────────────┴───────────┴───────────────────┘
✔ Are you sure you want to continue? (Y/n) · yes


Deployment completed.
Deploying root stack mylibrary [ ====================---------------
        amplify-mylibrary-dev-94433    AWS::CloudFormation::Stack     UPDAT
        authmylibrary8a675d6c          AWS::CloudFormation::Stack     CREAT
Deployed auth mylibrary8a675d6c [ ==================================
        UserPool                       AWS::Cognito::UserPool         CREAT
        UserPoolClientRole             AWS::IAM::Role                 CREAT
        UserPoolClient                 AWS::Cognito::UserPoolClient   CREAT
        UserPoolClientWeb              AWS::Cognito::UserPoolClient   CREAT
        IdentityPool                   AWS::Cognito::IdentityPool     CREAT
        IdentityPoolRoleMap            AWS::Cognito::IdentityPoolRol… CREAT

Deployment state saved successfully.


Browserslist: caniuse-lite is outdated. Please run:
  npx update-browserslist-db@latest
  Why you should do it regularly: https://github.com/browserslist/update-db#readme
No AppSync API configured. Please add an API
✔ Synced UI components.
```

これで、認証機能が追加されました。
あとは、実装をしていくのみです。
App.tsxを下記のように修正します。


```
import React from 'react';
import './App.css';
import { Authenticator, Flex, WithAuthenticatorProps, withAuthenticator } from '@aws-amplify/ui-react'

export function App({ signOut, user }: WithAuthenticatorProps) {
  return (
    <Flex direction="column" justifyContent="center">
      <Authenticator>
        {({ signOut, user }) => (
          <main>
            <h1>Hello {user?.username}</h1>
            <button onClick={signOut}>Sign out</button>
          </main>
        )}
      </Authenticator>
    </Flex>
  );
}

export default withAuthenticator(App);
```

実装はこれで完了。
では、まずはローカルで動作確認をしてみましょう。

ログイン画面が立ち上がるようになったので、`Create Account`タブから、EMail、電話番号、パスワードを入力して`Create Account`ボタンをクリックします。

![](/images/amplify-preview/2023-09-09-16-04-54.png)

EMailに送られてくるコードを入力する画面が表示されます。

![](/images/amplify-preview/2023-09-09-16-05-18.png)

しばらくすると、メールが受信され、記載されている確認コードを入力していきます。


![](/images/amplify-preview/2023-09-09-16-05-43.png)

![](/images/amplify-preview/2023-09-09-16-06-03.png)


ログインできました。

![](/images/amplify-preview/2023-09-09-16-34-48.png)

念のため、ログアウト、再ログインもしてみましょう。
右上の`ログアウト`ボタンをクリックします。

![](/images/amplify-preview/2023-09-09-16-35-39.png)

今度は先ほどアカウントを作成したので、`Sign In`タブの方から、メールアドレスとパスワードを入力していきます。

![](/images/amplify-preview/2023-09-09-16-36-01.png)

ログインできて、メインの画面が表示されました！

![](/images/amplify-preview/2023-09-09-16-36-16.png)

## いよいよプレビュー機能を確認！
ここまで修正した実装をコミットし、Githubにプルリクエストを作成します。

![](/images/amplify-preview/2023-09-09-16-38-55.png)


おりょ！？待てど暮らせど環境が構築されない・・

![](/images/amplify-preview/2023-09-09-16-40-55.png)

AWSのドキュメントをよーく読んでみると、、まさかのプライベートリポジトリ？？
ここで作成していたリポジトリはパブリックにしていたので、プライベートに変更してみることにします。
プライベートに変更ってできるのか？？

![](/images/amplify-preview/2023-09-09-16-48-22.png)

調べてみると、どうやらできそうです。
リポジトリの設定に`Change repository visibility`という項目があったので、ここからpublic -> privateに変更していきます。

![](/images/amplify-preview/2023-09-09-16-50-17.png)

おおっ！もう一度プルリク作り直したら、動き始めたーー！
![](/images/amplify-preview/2023-09-09-16-54-32.png)

ちょっと時間はかかりましたが、この通り、環境ができたようです。

![](/images/amplify-preview/2023-09-09-17-28-55.png)

バックエンド環境だけ、新しくできるんだー。。なるほど。

![](/images/amplify-preview/2023-09-09-17-29-56.png)

プレビューからアクセスすると、ログイン画面が表示されました。
バックエンドが新たに構築されているので、ローカルで作ったアカウントもない状態になっているようですね。
改めてアカウントを作成し、確認コードを入力する作業を終えると、メイン画面へのアクセスまでできるようになりました。

![](/images/amplify-preview/2023-09-09-17-30-49.png)

![](/images/amplify-preview/2023-09-09-17-33-18.png)

動作確認が完了したので、プルリクエストをマージしてクローズします。
プルリクがクローズされたら環境もきれいになくなってくれるはず。

まずは、プレビューがなくなりました。

![](/images/amplify-preview/2023-09-09-17-37-16.png)

バックエンド環境もなくなりました！

![](/images/amplify-preview/2023-09-09-17-37-58.png)

フロントはマージ後に再デプロイが自動で始まりました！！
おお、すごいっ！

![](/images/amplify-preview/2023-09-09-17-38-18.png)


![](/images/amplify-preview/2023-09-09-17-41-58.png)

## まとめ
というわけで、今回はここまでとなります。
教訓としては、Githubなら`プライベートリポジトリじゃないと、プレビュー機能が使えなかった`というところですかね。
Amplify、まだまだ全然使いこなせてないやい。。

また今後も、少しずつAmplify関連の備忘録をしたためていこうと思います。
