---
title: "AWS Amplify StudioでFigmaからReactアプリを作ってみた"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Figma", "Handson"]
published: true
---

## はじめに
下記の記事をもとに実際に手を動かしてみた記録をこの記事に残します。

https://aws.amazon.com/jp/blogs/news/aws-amplify-studio-figma-to-fullstack-react-app-with-minimal-programming/

それではさっそくやっていきましょう。

## バックエンドとフロントエンドを1つのGUI開発環境でビルドする

下記に記載されている通り、まずはやってみます。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-11-54.png)

`Deploy with Amplify Hosting`ボタンをクリックすると、新しいタブに下記の画面が表示されます。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-13-07.png)

> このワークフローは、GitHubのサンプルリポジトリをフォークして、
> 構成済みのバックエンドが含まれた新しいAmplifyアプリケーションをデプロイします。

なんですって！？
とにかく続けてみましょう。
`GitHub に接続`ボタンをクリックします。
すると、こんな画面が表示されました。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-15-48.png)

`サービスロールを選択`にてロールを選択します。
ハンズオンなので、`新しいロールを作成`ボタンにて新しいロールを作っちゃいます。
`新しいロールを作成`ボタンをクリックすると、新しいタブに下記の画面が表示されます。
そのまま`次のステップ: アクセス権限`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-20-31.png)

この画面もそのまま`次のステップ: タグ`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-21-35.png)

タグも、今回はハンズオンなので、そのまま次に進めます。`次のステップ: 確認`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-22-36.png)

ロールも特にデフォルトのまま行きます。
`ロールの作成`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-23-29.png)

新しいロールが作成できました！
ここから`アプリケーションをデプロイ`画面に戻ります。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-24-42.png)

先ほど作成したロールを設定して、`保存してデプロイ`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-26-16.png)

アプリケーションを作成しています。少し待つようです。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-26-53.png)


できました！
引き続き、`続行`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-59-21.png)

`Backend environments`タブを選択して、`Get started`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-00-09.png)


![](/images/handson-amplify-studio-figma-01/2023-03-21-17-01-32.png)


`Studio を起動する`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-04-51.png)

`Amplify Studio`が起動した！

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-05-57.png)

記事に載っている通り、`Data`を開くと`Home`というデータモデルができてる！

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-06-32.png)


## Contentメニューを使ってランダムなシードデータを生成する

記事に書いてある通り進めてみます。`Content`を開いてみます。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-08-36.png)

`Actions > Auto-generate data`を選択します。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-11-16.png)

`How many rows of data do you want to generate? (1-100)`には`5`を入力します。
`Add constraint`ボタンをクリックして、`Field Name`で`address`, `Range/setting`で`Street address`を選択し、最後に`Generate Data`をクリックします。そうするとランダムデータが生成されるようです。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-13-46.png)

ランダムデータが生成されました。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-14-19.png)

## タンダムデータに画像を設定する
作成したランダムデータに画像を設定します。
`Data Manager`の画面で編集したい行を選択すると編集ダイアログが表示されるので、そこに画像のURLを記載します。
記事では、[Unsplash’s random photo generator](https://source.unsplash.com/random)を使うとあるので、それを使ってやってみます。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-49-07.png)

出来上がりはこんな感じ。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-50-50.png)


## Figmaを使ってみる

次にFigmaを扱います。

:::message
事前にfigmaのアカウントを登録する必要があるようです。
:::

Figmaの`Search files, teams, or people`の検索入力のところに`AWS Amplify UI Kit`と入力して検索を行います。
`AWS Amplify UI Kit`が出てくるのでそれを開いて`Get Copy`にて複製します。

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-46-58.png)


![](/images/handson-amplify-studio-figma-01/2023-03-21-16-49-40.png)

`Pages > Primitives`を選択すると下記の画面に切り替わります。
`Primitives`はソースコード、`My Conponents`はプリビルドされたもののようです（使い分けがまだ分かっていない）。
今回は`My Components`の方を使うのか。。

Primitives:

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-50-25.png)

My Components:

![](/images/handson-amplify-studio-figma-01/2023-03-21-16-52-55.png)


右上の`Share`ボタンをクリックして、リンクをコピーします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-20-40.png)

`Copy link`ボタンをクリックするとコピーされます。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-20-59.png)

次に、`Amplify Studio`に戻りまして、`UI Library`を選択します。
右上に`Sync with Figma`ボタンがあるのでこれをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-27-05.png)

`② Paste your Figma file link`ここに先ほどコピーしたFigmaのリンクを貼り付けます。
貼り付けたら`Continue`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-27-59.png)

`許可しますか？`と聞かれるので`Allow access`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-29-26.png)

フォー何やら、取り込まれましたぞ！
あ、これだけじゃダメらしい。右上の`Accept all changes`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-30-34.png)

さらに個別に`Accept`していくか全て`Accept all`が必要なようです。
今回はハンズオンということもあって、全て受け入れてしまいます。

`Accept all`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-33-57.png)

取り込み完了しました！

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-34-25.png)

取り込んだコンポーネントから、`StandardCard`を使ってこの後進めてみます。
`StandardCard`を選択したら、`Configure`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-36-02.png)

ここで、コンポーネントの各要素とデータモデルを紐づけるのか！

適当にやってみます。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-41-53.png)

おお！できた。
`Shuffle preview data`ボタンをクリックするとランダムに作成したデータのどれかに切り替えてくれるようです。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-52-23.png)

## コレクションを作成する

右上の`Create collection`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-51-36.png)

コレクションの名前はいったんデフォルトのままで`Create`ボタンをクリックします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-53-51.png)



![](/images/handson-amplify-studio-figma-01/2023-03-21-17-54-34.png)

`Layout`を色々いじることができるようです。`List`から`Grid`にして`Columns`を`3`にしたり、マージンを設定したりしてみました。

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-55-34.png)


並び順も変えられるようです。
`Add sort`をクリックすると、どの項目でソートするかを設定できます。ほぇ〜

![](/images/handson-amplify-studio-figma-01/2023-03-21-17-57-09.png)

## React App に pullする

記事に載っている通り、githubリポジトリからcloneします。

次に、下記をインストールします。

```
npm install -g @aws-amplify/cli
```

```
% npm install -g @aws-amplify/cli

added 26 packages in 40s

7 packages are looking for funding
  run `npm fund` for details
```


次に、全てのnpm依存関係をローカルにインストールします。

```
npm install
```

```
% npm install
npm WARN ERESOLVE overriding peer dependency
npm WARN While resolving: jest-pnp-resolver@1.2.2
npm WARN Found: jest-resolve@26.6.0
npm WARN node_modules/jest-pnp-resolver/node_modules/jest-resolve
npm WARN 
npm WARN Could not resolve dependency:
npm WARN peerOptional jest-resolve@"*" from jest-pnp-resolver@1.2.2
npm WARN node_modules/jest-pnp-resolver
npm WARN   jest-pnp-resolver@"^1.2.2" from jest-resolve@26.6.0
npm WARN   node_modules/jest-pnp-resolver/node_modules/jest-resolve
npm WARN   2 more (jest-resolve, jest-resolve)
npm WARN ERESOLVE overriding peer dependency
npm WARN While resolving: @babel/plugin-proposal-nullish-coalescing-operator@7.12.13
npm WARN Found: @babel/core@7.12.17
npm WARN node_modules/babel-preset-react-app/node_modules/@babel/preset-env/node_modules/@babel/plugin-proposal-nullish-coalescing-operator/node_modules/@babel/core
npm WARN 
npm WARN Could not resolve dependency:
npm WARN peer @babel/core@"^7.0.0-0" from @babel/plugin-proposal-nullish-coalescing-operator@7.12.13
npm WARN node_modules/babel-preset-react-app/node_modules/@babel/preset-env/node_modules/@babel/plugin-proposal-nullish-coalescing-operator
npm WARN   @babel/plugin-proposal-nullish-coalescing-operator@"^7.12.1" from @babel/preset-env@7.12.1
npm WARN   node_modules/babel-preset-react-app/node_modules/@babel/preset-env
npm WARN ERESOLVE overriding peer dependency
npm WARN While resolving: @babel/plugin-proposal-numeric-separator@7.12.13
npm WARN Found: @babel/core@7.12.17
npm WARN node_modules/babel-preset-react-app/node_modules/@babel/preset-env/node_modules/@babel/plugin-proposal-numeric-separator/node_modules/@babel/core
npm WARN 
npm WARN Could not resolve dependency:
npm WARN peer @babel/core@"^7.0.0-0" from @babel/plugin-proposal-numeric-separator@7.12.13
npm WARN node_modules/babel-preset-react-app/node_modules/@babel/preset-env/node_modules/@babel/plugin-proposal-numeric-separator
npm WARN   @babel/plugin-proposal-numeric-separator@"^7.12.1" from @babel/preset-env@7.12.1
npm WARN   node_modules/babel-preset-react-app/node_modules/@babel/preset-env
npm WARN ERESOLVE overriding peer dependency
npm WARN While resolving: @babel/plugin-proposal-optional-chaining@7.12.17
npm WARN Found: @babel/core@7.12.17
npm WARN node_modules/babel-preset-react-app/node_modules/@babel/preset-env/node_modules/@babel/plugin-proposal-optional-chaining/node_modules/@babel/core
npm WARN 
npm WARN Could not resolve dependency:
npm WARN peer @babel/core@"^7.0.0-0" from @babel/plugin-proposal-optional-chaining@7.12.17
npm WARN node_modules/babel-preset-react-app/node_modules/@babel/preset-env/node_modules/@babel/plugin-proposal-optional-chaining
npm WARN   @babel/plugin-proposal-optional-chaining@"^7.12.1" from @babel/preset-env@7.12.1
npm WARN   node_modules/babel-preset-react-app/node_modules/@babel/preset-env
npm WARN ERESOLVE overriding peer dependency
npm WARN While resolving: @babel/plugin-transform-react-display-name@7.12.13
npm WARN Found: @babel/core@7.12.17
npm WARN node_modules/babel-preset-react-app/node_modules/@babel/preset-react/node_modules/@babel/plugin-transform-react-display-name/node_modules/@babel/core
npm WARN 
npm WARN Could not resolve dependency:
npm WARN peer @babel/core@"^7.0.0-0" from @babel/plugin-transform-react-display-name@7.12.13
npm WARN node_modules/babel-preset-react-app/node_modules/@babel/preset-react/node_modules/@babel/plugin-transform-react-display-name
npm WARN   @babel/plugin-transform-react-display-name@"^7.12.1" from @babel/preset-react@7.12.1
npm WARN   node_modules/babel-preset-react-app/node_modules/@babel/preset-react
npm WARN deprecated chokidar@2.1.8: Chokidar 2 will break on node v14+. Upgrade to chokidar 3 with 15x less dependencies.
npm WARN deprecated fsevents@1.2.13: fsevents 1 will break on node v14+ and could be using insecure binaries. Upgrade to fsevents 2.
npm WARN deprecated uuid@3.4.0: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
npm WARN deprecated request-promise-native@1.0.9: request-promise-native has been deprecated because it extends the now deprecated request package, see https://github.com/request/request/issues/3142
npm WARN deprecated sane@4.1.0: some dependency vulnerabilities fixed, support for node < 10 dropped, and newer ECMAScript syntax/features added
npm WARN deprecated rollup-plugin-babel@4.4.0: This package has been deprecated and is no longer maintained. Please use @rollup/plugin-babel.
npm WARN deprecated uglify-es@3.3.9: support for ECMAScript is superseded by `uglify-js` as of v3.13.0
npm WARN deprecated svgo@1.3.2: This SVGO version is no longer supported. Upgrade to v2.x.x.
npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
npm WARN deprecated querystring@0.2.0: The querystring API is considered Legacy. new code should use the URLSearchParams API instead.
npm WARN deprecated har-validator@5.1.5: this library is no longer supported
npm WARN deprecated flatten@1.0.3: flatten is deprecated in favor of utility frameworks such as lodash.
npm WARN deprecated babel-eslint@10.1.0: babel-eslint is now @babel/eslint-parser. This package will no longer receive updates.
npm WARN deprecated @hapi/topo@3.1.6: This version has been deprecated and is no longer supported or maintained
npm WARN deprecated @hapi/hoek@8.5.1: This version has been deprecated and is no longer supported or maintained
npm WARN deprecated @hapi/joi@15.1.1: Switch to 'npm install joi'
npm WARN deprecated @hapi/bourne@1.3.2: This version has been deprecated and is no longer supported or maintained
npm WARN deprecated @hapi/address@2.1.4: Moved to 'npm install @sideway/address'
npm WARN deprecated querystring@0.2.1: The querystring API is considered Legacy. new code should use the URLSearchParams API instead.
npm WARN deprecated core-js@2.6.12: core-js@<3.3 is no longer maintained and not recommended for usage due to the number of issues. Because of the V8 engine whims, feature detection in old core-js versions could cause a slowdown up to 100x even if nothing is polyfilled. Please, upgrade your dependencies to the actual version of core-js.
npm WARN deprecated uuid@3.3.2: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated

added 2397 packages, and audited 2398 packages in 58s

141 packages are looking for funding
  run `npm fund` for details

66 vulnerabilities (2 low, 12 moderate, 32 high, 20 critical)

To address issues that do not require attention, run:
  npm audit fix

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
```

次に、下記のコマンドを実行します。

```
amplify pull --appId <APP_ID> --envName <ENV>
```

`AWS Amplify`の画面に`ローカル設定手順`があった！

![](/images/handson-amplify-studio-figma-01/2023-03-21-18-06-52.png)

認証の画面が立ち上がるので、OKします。

![](/images/handson-amplify-studio-figma-01/2023-03-21-18-14-09.png)


次にエディタを選ぶよう言われるので、`Visual Studio Code`にしました。

```
Opening link: https://ap-northeast-1.admin.amplifyapp.com/admin/d1a6liks912dy1/devw/verify/?loginVersion=1
⠧ Confirm login in the browser or manually paste in your CLI login key:
Successfully received Amplify Studio tokens.
Amplify AppID found: d1a6liks912dy1. Amplify App name is: amplify-homes
Backend environment devw found in Amplify Console app: amplify-homes
? Choose your default editor: (Use arrow keys)
❯ Visual Studio Code 
  Android Studio 
  Xcode (macOS only) 
  Atom Editor 
  Sublime Text 
  IntelliJ IDEA 
  Vim (via Terminal, macOS only) 
(Move up and down to reveal more choices)
```

こちらはそのまま`javascript`で。

```
? Choose your default editor: Visual Studio Code
? Choose the type of app that you're building (Use arrow keys)
  android 
  flutter 
  ios 
❯ javascript 
```

こちらはそのまま`react`で。

```
? Choose the type of app that you're building javascript
Please tell us about your project
? What javascript framework are you using (Use arrow keys)
  angular 
  ember 
  ionic 
❯ react 
  react-native 
  vue 
  none 
```

こちらはそのまま`src`で。

```
? What javascript framework are you using react
? Source Directory Path:  (src) 
```

これもデフォルトのままで。

```
? Source Directory Path:  src
? Distribution Directory Path: (build) 
```

これもデフォルトのままで。

```
? Distribution Directory Path: build
? Build Command:  (npm run-script build) 
```

これもデフォルトのままで。

```
? Build Command:  npm run-script build
? Start Command: (npm run-script start) 
```

これもデフォルトのまま。

```
? Start Command: npm run-script start
✔ Synced UI components.
⚠️ UIBuilder components require version "^4.0.1" of "@aws-amplify/ui-react". You currently are on version "^2.13.0". Run `npm install "@aws-amplify/ui-react@^4.0.1"`. Required to leverage Amplify UI primitives, and Amplify Studio component helper functions.
⚠️ UIBuilder components require version "^5.0.2" of "aws-amplify". You currently are on version "^4.3.8". Run `npm install "aws-amplify@^5.0.2"`. Required to leverage DataStore.
✅ GraphQL schema compiled successfully.

Edit your schema at /Users/h.sato/amplify-homes/amplify/backend/api/amplifyhomes/schema.graphql or place .graphql files in a directory at /Users/h.sato/amplify-homes/amplify/backend/api/amplifyhomes/schema
Successfully generated models. Generated models can be found in /Users/h.sato/amplify-homes/src
? Do you plan on modifying this backend? (Y/n) 
````

実行結果は下記のとおりです。

```
% amplify pull --appId XXXXXXXXX --envName XXXX
Opening link: https://ap-northeast-1.admin.amplifyapp.com/admin/d1a6liks912dy1/devw/verify/?loginVersion=1
⠧ Confirm login in the browser or manually paste in your CLI login key:
Successfully received Amplify Studio tokens.
Amplify AppID found: d1a6liks912dy1. Amplify App name is: amplify-homes
Backend environment devw found in Amplify Console app: amplify-homes
? Choose your default editor: Visual Studio Code
? Choose the type of app that you're building javascript
Please tell us about your project
? What javascript framework are you using react
? Source Directory Path:  src
? Distribution Directory Path: build
? Build Command:  npm run-script build
? Start Command: npm run-script start
✔ Synced UI components.
⚠️ UIBuilder components require version "^4.0.1" of "@aws-amplify/ui-react". You currently are on version "^2.13.0". Run `npm install "@aws-amplify/ui-react@^4.0.1"`. Required to leverage Amplify UI primitives, and Amplify Studio component helper functions.
⚠️ UIBuilder components require version "^5.0.2" of "aws-amplify". You currently are on version "^4.3.8". Run `npm install "aws-amplify@^5.0.2"`. Required to leverage DataStore.
✅ GraphQL schema compiled successfully.

Edit your schema at /Users/h.sato/amplify-homes/amplify/backend/api/amplifyhomes/schema.graphql or place .graphql files in a directory at /Users/h.sato/amplify-homes/amplify/backend/api/amplifyhomes/schema
Successfully generated models. Generated models can be found in /Users/h.sato/amplify-homes/src
? Do you plan on modifying this backend? Yes
⠸ Building resource api/amplifyhomes✅ GraphQL schema compiled successfully.

Edit your schema at /Users/h.sato/amplify-homes/amplify/backend/api/amplifyhomes/schema.graphql or place .graphql files in a directory at /Users/h.sato/amplify-homes/amplify/backend/api/amplifyhomes/schema
✔ Successfully pulled backend environment devw from the cloud.
✅ 

✅ Successfully pulled backend environment devw from the cloud.
Run 'amplify pull' to sync future upstream changes.

✔ Synced UI components.
⚠️ UIBuilder components require version "^4.0.1" of "@aws-amplify/ui-react". You currently are on version "^2.13.0". Run `npm install "@aws-amplify/ui-react@^4.0.1"`. Required to leverage Amplify UI primitives, and Amplify Studio component helper functions.
⚠️ UIBuilder components require version "^5.0.2" of "aws-amplify". You currently are on version "^4.3.8". Run `npm install "aws-amplify@^5.0.2"`. Required to leverage DataStore.
```

次にUIコンポーネントをインポートしていきます。

```js: app.js
import './App.css';
import { NewHomes, NavBar, MarketingFooter } from './ui-components';

function App() {
  return (
    <div className="App">
      <NavBar/>
      <NewHomes/>
      <MarketingFooter/>
    </div>
  );
}

export default App;
```

ここでローカルで動かしてみましょう。

```
npm run start
```

あれ？動かんぞ！？

```
% npm run start

> amplify-homes@0.1.0 start
> react-scripts start

node:internal/modules/cjs/loader:571
      throw e;
      ^

Error [ERR_PACKAGE_PATH_NOT_EXPORTED]: Package subpath './lib/tokenize' is not defined by "exports" in /Users/h.sato/amplify-homes/node_modules/postcss-safe-parser/node_modules/postcss/package.json
    at new NodeError (node:internal/errors:399:5)
    at exportsNotFound (node:internal/modules/esm/resolve:361:10)
    at packageExportsResolve (node:internal/modules/esm/resolve:697:9)
    at resolveExports (node:internal/modules/cjs/loader:565:36)
    at Module._findPath (node:internal/modules/cjs/loader:634:31)
    at Module._resolveFilename (node:internal/modules/cjs/loader:1061:27)
    at Module._load (node:internal/modules/cjs/loader:920:27)
    at Module.require (node:internal/modules/cjs/loader:1141:19)
    at require (node:internal/modules/cjs/helpers:110:18)
    at Object.<anonymous> (/Users/h.sato/amplify-homes/node_modules/postcss-safe-parser/lib/safe-parser.js:1:17) {
  code: 'ERR_PACKAGE_PATH_NOT_EXPORTED'
}

Node.js v18.15.0
```

とりあえず、npmパッケージをアップデートしてみた。

```
npm update
```

これで、解消できたので、改めて`npm run start`します。
が、どうもローカルにインストールされているnodejsのバージョンが新しすぎるみたい。

```
Starting the development server...

Error: error:0308010C:digital envelope routines::unsupported
    at new Hash (node:internal/crypto/hash:71:19)
    at Object.createHash (node:crypto:133:10)
    at module.exports (/Users/h.sato/amplify-homes/node_modules/webpack/lib/util/createHash.js:135:53)
    at NormalModule._initBuildHash (/Users/h.sato/amplify-homes/node_modules/webpack/lib/NormalModule.js:417:16)
    at handleParseError (/Users/h.sato/amplify-homes/node_modules/webpack/lib/NormalModule.js:471:10)
    at /Users/h.sato/amplify-homes/node_modules/webpack/lib/NormalModule.js:503:5
    at /Users/h.sato/amplify-homes/node_modules/webpack/lib/NormalModule.js:358:12
    at /Users/h.sato/amplify-homes/node_modules/loader-runner/lib/LoaderRunner.js:373:3
    at iterateNormalLoaders (/Users/h.sato/amplify-homes/node_modules/loader-runner/lib/LoaderRunner.js:214:10)
    at iterateNormalLoaders (/Users/h.sato/amplify-homes/node_modules/loader-runner/lib/LoaderRunner.js:221:10)
/Users/h.sato/amplify-homes/node_modules/react-scripts/scripts/start.js:19
  throw err;
  ^

Error: error:0308010C:digital envelope routines::unsupported
    at new Hash (node:internal/crypto/hash:71:19)
    at Object.createHash (node:crypto:133:10)
    at module.exports (/Users/h.sato/amplify-homes/node_modules/webpack/lib/util/createHash.js:135:53)
    at NormalModule._initBuildHash (/Users/h.sato/amplify-homes/node_modules/webpack/lib/NormalModule.js:417:16)
    at /Users/h.sato/amplify-homes/node_modules/webpack/lib/NormalModule.js:452:10
    at /Users/h.sato/amplify-homes/node_modules/webpack/lib/NormalModule.js:323:13
    at /Users/h.sato/amplify-homes/node_modules/loader-runner/lib/LoaderRunner.js:367:11
    at /Users/h.sato/amplify-homes/node_modules/loader-runner/lib/LoaderRunner.js:233:18
    at context.callback (/Users/h.sato/amplify-homes/node_modules/loader-runner/lib/LoaderRunner.js:111:13)
    at /Users/h.sato/amplify-homes/node_modules/babel-loader/lib/index.js:59:103 {
  opensslErrorStack: [ 'error:03000086:digital envelope routines::initialization error' ],
  library: 'digital envelope routines',
  reason: 'unsupported',
  code: 'ERR_OSSL_EVP_UNSUPPORTED'
}

Node.js v18.15.0
```

nodeのバージョンを調整して再挑戦！

うーん、画面表示できたけれども、画像が表示されんね。。

![](/images/handson-amplify-studio-figma-01/2023-03-21-18-57-57.png)

とりあえず、今回は時間の都合でここまでとしました。