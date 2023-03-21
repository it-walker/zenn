---
title: "AWS Amplify ハンズオンをやってみた（4）"
emoji: "😊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Handson"]
published: true
---

## はじめに
この記事は、`AWS Amplifyのハンズオンやってみた（3）`のつづきです。
下記リンクの`05 AWS Amplify のハンズオン（FE/API/DB 編）`の動画を見ながら作業しています。

https://pages.awscloud.com/JAPAN-event-OE-Hands-on-for-Beginners-amplify-2022-confirmation-774.html


## 認証周りの設定
認証周りの設定をやっていきます。
下記のコマンドをCloud9のターミナルから実行します。
カレントディレクトリは作成したアプリのディレクトリです。

```
amplify add auth
```

認証に関する設定ですが、ここでは、デフォルトの設定で進めます。

```
amplify add auth
Using service: Cognito, provided by: awscloudformation
 
 The current configured provider is Amazon Cognito. 
 
 Do you want to use the default authentication and security configuration? (Use arrow keys)
❯ Default configuration 
  Default configuration with Social Provider (Federation) 
  Manual configuration 
  I want to learn more. 
```

次はサインインの方法について問われているので、今回は`Username`を使う方法で進めます。

```
 Do you want to use the default authentication and security configuration? Default configuration
 Warning: you will not be able to edit these selections. 
 How do you want users to be able to sign in? (Use arrow keys)
❯ Username 
  Email 
  Phone Number 
  Email or Phone Number 
  I want to learn more.
```

詳細設定は今回は行わないため、`No`を選択します。

```
 How do you want users to be able to sign in? Username
 Do you want to configure advanced settings? (Use arrow keys)
❯ No, I am done. 
  Yes, I want to make some additional changes. 
```

最終的な実行結果はこんな感じです。

```
amplify add auth
Using service: Cognito, provided by: awscloudformation
 
 The current configured provider is Amazon Cognito. 
 
 Do you want to use the default authentication and security configuration? Default configuration
 Warning: you will not be able to edit these selections. 
 How do you want users to be able to sign in? Username
 Do you want to configure advanced settings? No, I am done.
✅ Successfully added auth resource todoappf5a89554 locally

✅ Some next steps:
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud
```

ここで`amplify status`コマンドを実行して確認してみます。

```
amplify status
```

`Auth`が追加されていますね。

```
amplify status

    Current Environment: dev
    
┌──────────┬─────────────────┬───────────┬───────────────────┐
│ Category │ Resource name   │ Operation │ Provider plugin   │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Auth     │ todoappf5a89554 │ Create    │ awscloudformation │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Api      │ todoapp         │ No Change │ awscloudformation │
└──────────┴─────────────────┴───────────┴───────────────────┘

GraphQL endpoint: https://ihpelgfzvvgqvd6txi4mwsgppe.appsync-api.ap-northeast-2.amazonaws.com/graphql
GraphQL API KEY: da2-g4yfnrnkirg2rmusba2j5dxkuq

GraphQL transformer version: 2
```

確認できたので次は`amplify push`を実行していきます。

```
amplify push
```

実行した結果は下記の通り。

```
$ amplify push
⠙ Fetching updates to backend environment: dev from the cloud.
⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

⠹ Fetching updates to backend environment: dev from the cloud.✅ GraphQL schema compiled successfully.

Edit your schema at /home/ec2-user/environment/todoapp/amplify/backend/api/todoapp/schema.graphql or place .graphql files in a directory at /home/ec2-user/environment/todoapp/amplify/backend/api/todoapp/schema
✔ Successfully pulled backend environment dev from the cloud.

    Current Environment: dev
    
┌──────────┬─────────────────┬───────────┬───────────────────┐
│ Category │ Resource name   │ Operation │ Provider plugin   │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Auth     │ todoappf5a89554 │ Create    │ awscloudformation │
├──────────┼─────────────────┼───────────┼───────────────────┤
│ Api      │ todoapp         │ No Change │ awscloudformation │
└──────────┴─────────────────┴───────────┴───────────────────┘
✔ Are you sure you want to continue? (Y/n) · yes

Deployment completed.
Deploying root stack todoapp [ ===========================------------- ] 2/3
        amplify-todoapp-dev-60136      AWS::CloudFormation::Stack     UPDATE_COMPLETE_CLEANUP_IN_PR… Sun Mar 19 2023 07:35:55…     
        apitodoapp                     AWS::CloudFormation::Stack     UPDATE_COMPLETE                Sun Mar 19 2023 07:33:20…     
        authtodoappf5a89554            AWS::CloudFormation::Stack     CREATE_COMPLETE                Sun Mar 19 2023 07:35:37…     
Deployed auth todoappf5a89554 [ ======================================== ] 10/10
        UserPool                       AWS::Cognito::UserPool         CREATE_COMPLETE                Sun Mar 19 2023 07:33:09…     
        UserPoolClientWeb              AWS::Cognito::UserPoolClient   CREATE_COMPLETE                Sun Mar 19 2023 07:33:13…     
        UserPoolClient                 AWS::Cognito::UserPoolClient   CREATE_COMPLETE                Sun Mar 19 2023 07:33:13…     
        UserPoolClientRole             AWS::IAM::Role                 CREATE_COMPLETE                Sun Mar 19 2023 07:33:51…     
        UserPoolClientLambda           AWS::Lambda::Function          CREATE_COMPLETE                Sun Mar 19 2023 07:34:03…     
        UserPoolClientLambdaPolicy     AWS::IAM::Policy               CREATE_COMPLETE                Sun Mar 19 2023 07:34:40…     
        UserPoolClientLogPolicy        AWS::IAM::Policy               CREATE_COMPLETE                Sun Mar 19 2023 07:35:18…     
        UserPoolClientInputs           Custom::LambdaCallout          CREATE_COMPLETE                Sun Mar 19 2023 07:35:24…     
        IdentityPool                   AWS::Cognito::IdentityPool     CREATE_COMPLETE                Sun Mar 19 2023 07:35:30…     
        IdentityPoolRoleMap            AWS::Cognito::IdentityPoolRol… CREATE_IN_PROGRESS             Sun Mar 19 2023 07:35:32…     

Deployment state saved successfully.

GraphQL transformer version: 2
```

### ログイン画面の作成

`@aws-amplify/ui-react`をインストールします。

```
$ npm install @aws-amplify/ui-react
```

```
$ npm install @aws-amplify/ui-react

added 160 packages, and audited 2785 packages in 34s

263 packages are looking for funding
  run `npm fund` for details

6 high severity vulnerabilities

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
```

次に`src/App.js`に下記のコードを追加します。

```
import { withAuthenticator, Button, Heading } from '@aws-amplify/ui-react';
import '@aws-amplify/ui-react/styles.css';
```

![](/images/aws-amplify-handson-04/2023-03-19-16-44-14.png)

次に`src/App.js`の`function`の引数のところを下記の記述に変更します。

```
/* src/App.js */
function App({ signOut, user }) { 
  // ... 
}
```


![](/images/aws-amplify-handson-04/2023-03-19-16-46-35.png)

次に、`return`部分を下記の記述に変更します。

```
// ...
return (
  <div style={styles.container}>
    <Heading level={1}>Hello {user.username}</Heading>
    <Button onClick={signOut}>Sign out</Button>
    <h2>Amplify Todos</h2>
//...
```

![](/images/aws-amplify-handson-04/2023-03-19-16-49-39.png)

最後に`src/App.js`の`export`文のところを下記に変更します。

```
export default withAuthenticator(App);
```

![](/images/aws-amplify-handson-04/2023-03-19-16-52-50.png)

実行してみましょう

```
npm start
```

サインインの画面が出てきました！！

![](/images/aws-amplify-handson-04/2023-03-19-16-54-17.png)


では、アカウントを作成してみましょう。
`Create Account`タブに切り替えて、アカウント情報を入力したら`Create Account`ボタンをクリックします。


![](/images/aws-amplify-handson-04/2023-03-19-16-59-14.png)


![](/images/aws-amplify-handson-04/2023-03-19-17-00-34.png)

メールを受信したら認証コードを入力します。

![](/images/aws-amplify-handson-04/2023-03-19-17-00-59.png)

おおーログインできたー

![](/images/aws-amplify-handson-04/2023-03-19-17-03-00.png)

## おまけ

`Heading` と `Button` という2つの Amplify UI コンポーネントを使用しています。また、`p`タグを`Text`、`input`を`TextFields`、`div`を`Views`に置き換えることで、残りのアプリをAmplify UIコンポーネントに変換することができます。
Amplify UIコンポーネントを使うことで、アプリ全体のスタイリング管理が容易になります。

まず、`Text`、`TextField`、`View`コンポーネントを追加します。

```
import { withAuthenticator, Button, Heading, Text, TextField, View } from '@aws-amplify/ui-react';
```

次に、下記のように置き換えます。

* `p` -> `Text`
* `input` -> `TextFields`
* `div` -> `Views`

```
  return (
    <View style={styles.container}>
      <Heading level={1}>Hello {user.username}</Heading>
      <Button onClick={signOut}>Sign out</Button>
      <h2>Amplify Todos</h2>
      <TextField
        onChange={event => setInput('name', event.target.value)}
        style={styles.input}
        value={formState.name}
        placeholder="Name"
      />
      <TextField
        onChange={event => setInput('description', event.target.value)}
        style={styles.input}
        value={formState.description}
        placeholder="Description"
      />
      <Button style={styles.button} onClick={addTodo}>Create Todo</Button>
      {
        todos.map((todo, index) => (
          <View key={todo.id ? todo.id : index} style={styles.todo}>
            <Text style={styles.todoName}>{todo.name}</Text>
            <Text style={styles.todoDescription}>{todo.description}</Text>
          </View>
        ))
      }
    </View>
  )
```
