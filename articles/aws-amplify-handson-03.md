---
title: "AWS Amplifyのハンズオンやってみた（3）"
emoji: "🐷"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Handson"]
published: true
---

##　はじめに
この記事は、`AWS Amplifyのハンズオンやってみた（2）`のつづきです。
下記リンクの`04 AWS Amplify のハンズオン（FE/API/DB 編）`の動画を見ながら作業しています。

https://pages.awscloud.com/JAPAN-event-OE-Hands-on-for-Beginners-amplify-2022-confirmation-774.html

## データベースのプロビジョニング

`GraphQL API`を追加し、自動的にデータベースをプロビジョニングします。
下記のコマンドを実行します。
作業ディレクトリは前回の`react-amplified`です。

```
amplify add api
```

今回は`GraphQL`を選択します。そのまま`Enter`を押します。

```
? Select from one of the below mentioned services: (Use arrow keys)
❯ GraphQL
  REST
```

下記の部分はそのまま`Enter`を押します。

```
? Here is the GraphQL API that we will create. Select a setting to edit or continue (Use arrow keys)
  Name: reactamplified
  Authorization modes: API key (default, expiration time: 7 days from now)
  Conflict detection (required for DataStore): Disabled
❯ Continue
```

スキーマのテンプレートについても、デフォルトの`Single object with fileds`で進めます。`Enter`を押します。

```
? Here is the GraphQL API that we will create. Select a setting to edit or continue Continue
? Choose a schema template: (Use arrow keys)
❯ Single object with fields (e.g., “Todo” with ID, name, description)
  One-to-many relationship (e.g., “Blogs” with “Posts” and “Comments”)
  Blank Schema
```

スキーマを今変更するかを聞かれますが、`n`を選択します。

```
⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema.graphql or place .graphql files in a directory at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema
? Do you want to edit the schema now? (Y/n) ‣
```

```
✔ Do you want to edit the schema now? (Y/n) · no
✅ Successfully added resource reactamplified locally

✅ Some next steps:
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud
```

ここで設定を確認するために、下記のコマンドを実行します。

```
amplify status
```

```
$ amplify status

    Current Environment: dev

┌──────────┬────────────────┬───────────┬───────────────────┐
│ Category │ Resource name  │ Operation │ Provider plugin   │
├──────────┼────────────────┼───────────┼───────────────────┤
│ Api      │ reactamplified │ Create    │ awscloudformation │
└──────────┴────────────────┴───────────┴───────────────────┘

GraphQL transformer version: 2
```

`Operation`が`Create`というのは`作成待ち`という状態なので、まだ Amplify 上に反映されていないことがわかります。

実際に反映させるために、下記のコマンドを実行します。

```
amplify push
```

途中で聞かれるところは`Y`を選択します。

```
$ amplify push
⠧ Building resource api/reactamplified
⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema.graphql or place .graphql files in a directory at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema
✔ Successfully pulled backend environment dev from the cloud.
⠦ Building resource api/reactamplified
⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema.graphql or place .graphql files in a directory at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema

    Current Environment: dev

┌──────────┬────────────────┬───────────┬───────────────────┐
│ Category │ Resource name  │ Operation │ Provider plugin   │
├──────────┼────────────────┼───────────┼───────────────────┤
│ Api      │ reactamplified │ Create    │ awscloudformation │
└──────────┴────────────────┴───────────┴───────────────────┘
✔ Are you sure you want to continue? (Y/n) · yes

⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema.graphql or place .graphql files in a directory at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema
⠧ Building resource api/reactamplified
⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema.graphql or place .graphql files in a directory at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema
? Do you want to generate code for your newly created GraphQL API Yes
? Choose the code generation language target typescript
? Enter the file name pattern of graphql queries, mutations and subscriptions src/graphql/**/*.ts
? Do you want to generate/update all possible GraphQL operations - queries, mutations and subscriptions Yes
? Enter maximum statement depth [increase from default if your schema is deeply nested] 2
? Enter the file name for the generated code src/API.ts

Deployment completed.
Deploying root stack reactamplified [ ====================-------------------- ] 1/2
        amplify-reactamplified-dev-40… AWS::CloudFormation::Stack     UPDATE_IN_PROGRESS             Sun Mar 19 2023 04:42:42…
        apireactamplified              AWS::CloudFormation::Stack     CREATE_COMPLETE                Sun Mar 19 2023 04:46:20…
Deployed api reactamplified [ ======================================== ] 6/6
        GraphQLAPI                     AWS::AppSync::GraphQLApi       CREATE_COMPLETE                Sun Mar 19 2023 04:42:56…
        GraphQLAPIDefaultApiKey215A6D… AWS::AppSync::ApiKey           CREATE_COMPLETE                Sun Mar 19 2023 04:43:00…
        GraphQLAPITransformerSchema3C… AWS::AppSync::GraphQLSchema    CREATE_COMPLETE                Sun Mar 19 2023 04:44:02…
        GraphQLAPINONEDS95A13CF0       AWS::AppSync::DataSource       CREATE_COMPLETE                Sun Mar 19 2023 04:43:00…
        Todo                           AWS::CloudFormation::Stack     CREATE_COMPLETE                Sun Mar 19 2023 04:45:43…
        CustomResourcesjson            AWS::CloudFormation::Stack     CREATE_IN_PROGRESS             Sun Mar 19 2023 04:45:45…

✔ Generated GraphQL operations successfully and saved at src/graphql
✔ Code generated successfully and saved in file src/API.ts
Deployment state saved successfully.

GraphQL endpoint: https://73jvf2h6svdgfcn4462z52thpy.appsync-api.ap-northeast-2.amazonaws.com/graphql
GraphQL API KEY: da2-azemy2tpszevvgkgjufhlp6nxy

GraphQL transformer version: 2
```

次は`src/App.js`を開いて中身を下記に置き換えます。

```
/* src/App.js */
import React, { useEffect, useState } from 'react'
import { Amplify, API, graphqlOperation } from 'aws-amplify'
import { createTodo } from './graphql/mutations'
import { listTodos } from './graphql/queries'

import awsExports from "./aws-exports";
Amplify.configure(awsExports);

const initialState = { name: '', description: '' }

const App = () => {
  const [formState, setFormState] = useState(initialState)
  const [todos, setTodos] = useState([])

  useEffect(() => {
    fetchTodos()
  }, [])

  function setInput(key, value) {
    setFormState({ ...formState, [key]: value })
  }

  async function fetchTodos() {
    try {
      const todoData = await API.graphql(graphqlOperation(listTodos))
      const todos = todoData.data.listTodos.items
      setTodos(todos)
    } catch (err) { console.log('error fetching todos') }
  }

  async function addTodo() {
    try {
      if (!formState.name || !formState.description) return
      const todo = { ...formState }
      setTodos([...todos, todo])
      setFormState(initialState)
      await API.graphql(graphqlOperation(createTodo, {input: todo}))
    } catch (err) {
      console.log('error creating todo:', err)
    }
  }

  return (
    <div style={styles.container}>
      <h2>Amplify Todos</h2>
      <input
        onChange={event => setInput('name', event.target.value)}
        style={styles.input}
        value={formState.name}
        placeholder="Name"
      />
      <input
        onChange={event => setInput('description', event.target.value)}
        style={styles.input}
        value={formState.description}
        placeholder="Description"
      />
      <button style={styles.button} onClick={addTodo}>Create Todo</button>
      {
        todos.map((todo, index) => (
          <div key={todo.id ? todo.id : index} style={styles.todo}>
            <p style={styles.todoName}>{todo.name}</p>
            <p style={styles.todoDescription}>{todo.description}</p>
          </div>
        ))
      }
    </div>
  )
}

const styles = {
  container: { width: 400, margin: '0 auto', display: 'flex', flexDirection: 'column', justifyContent: 'center', padding: 20 },
  todo: {  marginBottom: 15 },
  input: { border: 'none', backgroundColor: '#ddd', marginBottom: 10, padding: 8, fontSize: 18 },
  todoName: { fontSize: 20, fontWeight: 'bold' },
  todoDescription: { marginBottom: 0 },
  button: { backgroundColor: 'black', color: 'white', outline: 'none', fontSize: 18, padding: '12px 0px' }
}

export default App
```

保存し終わったら、`npm start`で動作を確認してみます。

```
npm start
```

なぜかうまくいかなくて、もう一度作り直したり、一からやり直したりしたのですが、書き方の問題でした。

`src/index.js`に追加した内容を先頭に追加したのですが、先頭ではなく、import 文の最後に追加すべきでした。
eslint で import 文より前に処理を書いてしまっている状態になっていたので、怒られていたようです。

こうすべきだった。

```
〜
import { Amplify } from 'aws-amplify';
import awsExports from './aws-exports';
Amplify.configure(awsExports);
```
