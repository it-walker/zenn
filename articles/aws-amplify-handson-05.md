---
title: "AWS Amplify ハンズオンをやってみた（5）"
emoji: "📌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Handson"]
published: false
---

## はじめに
この記事は、`AWS Amplify ハンズオンをやってみた（4）`のつづきです。
下記リンクの`06 AWS Amplify のハンズオン（Hosting 編）`の動画を見ながら作業しています。

https://pages.awscloud.com/JAPAN-event-OE-Hands-on-for-Beginners-amplify-2022-confirmation-774.html

## アプリのホスティング

アプリのホスティングをやっていきます。
静的ファイルのホスティング機能を追加していきます。

```
amplify add hosting
```

今回はそのままの選択でいきます。

```
$ amplify add hosting
? Select the plugin module to execute …  (Use arrow keys or type to filter)
❯ Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)
  Amazon CloudFront and S3
```

そのままの設定で行きます。

```
✔ Select the plugin module to execute · Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)
? Choose a type (Use arrow keys)
  Continuous deployment (Git-based deployments) 
❯ Manual deployment 
  Learn more 
```

実行した結果が下記になります。

```
$ amplify add hosting
✔ Select the plugin module to execute · Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)
? Choose a type Manual deployment

You can now publish your app using the following command:

Command: amplify publish
```


ここでステータスを確認してみましょう。

```
amplify status
```

Hostingが追加されたことが確認できました。

```
$ amplify status

    Current Environment: dev
    
┌──────────┬─────────────────┬───────────┬───────────────────┐
│ Category │ Resource name   │ Operation │ Provider plugin   │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Hosting  │ amplifyhosting  │ Create    │ awscloudformation │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Api      │ todoapp         │ No Change │ awscloudformation │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Auth     │ todoappf5a89554 │ No Change │ awscloudformation │
└──────────┴─────────────────┴───────────┴───────────────────┘

GraphQL endpoint: https://ihpelgfzvvgqvd6txi4mwsgppe.appsync-api.ap-northeast-2.amazonaws.com/graphql
GraphQL API KEY: da2-g4yfnrnkirg2rmusba2j5dxkuq

GraphQL transformer version: 2

No amplify console domain detected
```

次に下記コマンドを実行します。

```
amplify publish
```

確認して問題なければ`y`で`Enter`を押します。

```
$ amplify publish
⠸ Fetching updates to backend environment: dev from the cloud.
⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

⠼ Fetching updates to backend environment: dev from the cloud.✅ GraphQL schema compiled successfully.

Edit your schema at /home/ec2-user/environment/todoapp/amplify/backend/api/todoapp/schema.graphql or place .graphql files in a directory at /home/ec2-user/environment/todoapp/amplify/backend/api/todoapp/schema
✔ Successfully pulled backend environment dev from the cloud.

    Current Environment: dev
    
┌──────────┬─────────────────┬───────────┬───────────────────┐
│ Category │ Resource name   │ Operation │ Provider plugin   │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Hosting  │ amplifyhosting  │ Create    │ awscloudformation │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Api      │ todoapp         │ No Change │ awscloudformation │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Auth     │ todoappf5a89554 │ No Change │ awscloudformation │
└──────────┴─────────────────┴───────────┴───────────────────┘
? Are you sure you want to continue? (Y/n) ‣ 
```

実行した結果は下記の通り。


```
$ amplify publish
⠸ Fetching updates to backend environment: dev from the cloud.
⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

⠼ Fetching updates to backend environment: dev from the cloud.✅ GraphQL schema compiled successfully.

Edit your schema at /home/ec2-user/environment/todoapp/amplify/backend/api/todoapp/schema.graphql or place .graphql files in a directory at /home/ec2-user/environment/todoapp/amplify/backend/api/todoapp/schema
✔ Successfully pulled backend environment dev from the cloud.

    Current Environment: dev
    
┌──────────┬─────────────────┬───────────┬───────────────────┐
│ Category │ Resource name   │ Operation │ Provider plugin   │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Hosting  │ amplifyhosting  │ Create    │ awscloudformation │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Api      │ todoapp         │ No Change │ awscloudformation │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Auth     │ todoappf5a89554 │ No Change │ awscloudformation │
└──────────┴─────────────────┴───────────┴───────────────────┘
✔ Are you sure you want to continue? (Y/n) · yes

Deployment completed.
Deploying root stack todoapp [ ==============================---------- ] 3/4
        amplify-todoapp-dev-60136      AWS::CloudFormation::Stack     UPDATE_COMPLETE_CLEANUP_IN_PR… Sun Mar 19 2023 12:59:16…     
        apitodoapp                     AWS::CloudFormation::Stack     UPDATE_COMPLETE                Sun Mar 19 2023 12:59:13…     
        hostingamplifyhosting          AWS::CloudFormation::Stack     CREATE_COMPLETE                Sun Mar 19 2023 12:59:02…     
        authtodoappf5a89554            AWS::CloudFormation::Stack     UPDATE_COMPLETE                Sun Mar 19 2023 12:58:53…     
Deployed hosting amplifyhosting [ ======================================== ] 1/1
        AmplifyBranch                  AWS::Amplify::Branch           CREATE_IN_PROGRESS             Sun Mar 19 2023 12:58:55…     

Deployment state saved successfully.

GraphQL transformer version: 2

Publish started for amplifyhosting

> todoapp@0.1.0 build
> react-scripts build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  260.13 kB  build/static/js/main.be276451.js
  33.22 kB   build/static/css/main.2a6eba90.css
  1.78 kB    build/static/js/787.b8fa26a9.chunk.js

The project was built assuming it is hosted at /.
You can control this with the homepage field in your package.json.

The build folder is ready to be deployed.
You may serve it with a static server:

  npm install -g serve
  serve -s build

Find out more about deployment here:

  https://cra.link/deployment

✔ Zipping artifacts completed.
✔ Deployment complete!
https://dev.d2qv1zj2kkkjd7.amplifyapp.com
```

上記の最後のURLにアクセスすると。。

![](/images/f2926e63cde7d6/2023-03-19-22-03-42.png)

できたー！
ばっちりタスクの追加もできることを確認！

![](/images/f2926e63cde7d6/2023-03-19-22-04-10.png)