---
title: "SNSログイン機能を実装してみた（３）"
emoji: "🌊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "SNS"]
published: true
---

## はじめに

前回、「SNS ログイン機能を実装してみた（２）」では、SNS ログイン機能の実装に再挑戦したのですが、これも見事に失敗に終わってしまいました。
もう少し粘って頑張ってみます。。

## 改めて認証機能を作り直してみる

ローカルから改めてコマンドから実行してみようと思います。

```
amplify auth remove
```

```
amplify auth remove

Only one option for [Choose the resource you would want to remove]. Selecting [mylibrary8a675d6c].

? Are you sure you want to delete the resource? This action deletes all files related to this resou
rce from the backend directory. Yes
✅ Successfully removed resource
```

一応確認で`amplify status`を実行しておきますか。

```
amplify status
```

```
amplify status

    Current Environment: dev

┌──────────┬───────────────────┬───────────┬───────────────────┐
│ Category │ Resource name     │ Operation │ Provider plugin   │
├──────────┼───────────────────┼───────────┼───────────────────┤
│ Auth     │ mylibrary8a675d6c │ Delete    │ awscloudformation │
└──────────┴───────────────────┴───────────┴───────────────────┘
```

削除状態で`amplify push`していきます。

```
amplify push
```

```
amplify push
✔ Successfully pulled backend environment dev from the cloud.

    Current Environment: dev

┌──────────┬───────────────────┬───────────┬───────────────────┐
│ Category │ Resource name     │ Operation │ Provider plugin   │
├──────────┼───────────────────┼───────────┼───────────────────┤
│ Auth     │ mylibrary8a675d6c │ Delete    │ awscloudformation │
└──────────┴───────────────────┴───────────┴───────────────────┘
✔ Are you sure you want to continue? (Y/n) · yes


Deployment completed.
Deploying root stack mylibrary [ ---------------------------------------- ] 0/1
        amplify-mylibrary-dev-94433    AWS::CloudFormation::Stack     UPDATE_COMPLETE_CLEANUP_IN

Deployment state saved successfully.


Browserslist: caniuse-lite is outdated. Please run:
  npx update-browserslist-db@latest
  Why you should do it regularly: https://github.com/browserslist/update-db#readme
No AppSync API configured. Please add an API
✔ Synced UI components.
```

これで認証機能が削除されました。

さて、ここから作り直していきます。

```
amplify add auth
```

### Do you want to use the default authentication and security configuration? (Use arrow keys)

Google でのログインを実装したいので、`Default configuration with Social Provider (Federation)`を選択します。

```
Do you want to use the default authentication and security configuration? (Use arrow keys)
❯ Default configuration
  Default configuration with Social Provider (Federation)
  Manual configuration
  I want to learn more.
```

### Do you want to use the default authentication and security configuration? Default configuration with Social Provider (Federation)

なんか怖いメッセージ出てるけど、大丈夫かな？？
とりあえず、`Username`のまま行ってみます。

```
 Do you want to use the default authentication and security configuration? Default configuration wi
th Social Provider (Federation)
 Warning: you will not be able to edit these selections.
 How do you want users to be able to sign in? (Use arrow keys)
❯ Username
  Email
  Phone Number
  Email or Phone Number
  I want to learn more.
```

### Do you want to configure advanced settings? (Use arrow keys)

ここも、そのまま`No, I am done.`で進めます。

```
How do you want users to be able to sign in? Username
Do you want to configure advanced settings? (Use arrow keys)
❯ No, I am done.
Yes, I want to make some additional changes.
```

### What domain name prefix do you want to use?

ここもデフォルトのまま進めます。

### Enter your redirect signin URI:

ローカルで実施を試すので、`http://localhost:3000/`を入力します。

### Do you want to add another redirect signin URI (y/N)

リダイレクトは不要なので、`N`

### Enter your redirect signout URI

ここもローカルで。

### Do you want to add another redirect signout URI

これは不要なので、`N`

### Select the social providers you want to configure for your user pool: (Press <space> to select, <a> to toggle all, <i> to invert selection)

ここは、`Google`を選択します。

```
Select the social providers you want to configure for your user pool: (Press <space> to select, <a
> to toggle all, <i> to invert selection)
❯◯ Facebook
 ◯ Google
 ◯ Login With Amazon
 ◯ Sign in with Apple
```

### 一応成功したみたい。

OAuth の設定があると思っていたのですが、これまでの中で設定済みなのでスキップされたのかな！？

```
 Select the social providers you want to configure for your user pool:
✅ Successfully added auth resource mylibrary18be8019 locally

✅ Some next steps:
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud
```

```
amplify status

    Current Environment: dev

┌──────────┬───────────────────┬───────────┬───────────────────┐
│ Category │ Resource name     │ Operation │ Provider plugin   │
├──────────┼───────────────────┼───────────┼───────────────────┤
│ Auth     │ mylibrary18be8019 │ Create    │ awscloudformation │
└──────────┴───────────────────┴───────────┴───────────────────┘
```

## ローカルで実行してみる

これでいいのか？と疑念を感じつつもまずはローカルで実行してみましょう。

![](/images/20230914-amplify-sns-login-03/2023-09-17-13-05-50.png)

あらら、悪化しちまったやないかいっ！

## Amplify Studio 見てみたら・・・

SNS の設定できてないじゃん。
ここまでで出た ↓ の意味ってそういうこと！？
ローカルからは作成できないってことなのかな。

```
Warning: you will not be able to edit these selections.
```

## やっと・・・

Amplify Studio の認証機能の設定のところに表示されている URL を Google Cloud の承認済みのリダイレクト URL に設定すればいいみたい。

![](/images/20230914-amplify-sns-login-03/2023-09-17-13-38-12.png)

![](/images/20230914-amplify-sns-login-03/2023-09-17-13-41-22.png)

ここまでできたら、改めて認証機能を`deploy`します。
`deploy`が完了したら、`amplify pull`を実行します。

![](/images/20230914-amplify-sns-login-03/2023-09-17-13-44-39.png)

![](/images/20230914-amplify-sns-login-03/2023-09-17-13-30-24.png)

ウォーできたーー！！

![](/images/20230914-amplify-sns-login-03/2023-09-17-13-36-37.png)
