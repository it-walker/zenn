---
title: "Amplifyで分析してみよう（Amazon pinpoint）"
emoji: "🐥"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Amplify", "Pinpoint"]
published: false
---

## さっそくやってみる

下記のコマンドで分析を追加してみます。

```
amplify add analytics
```

![](/images/aws-amplify-analytics-01/2023-06-06-12-54-43.png)

![](/images/aws-amplify-analytics-01/2023-06-06-12-56-22.png)

## ユーザーのイベントを登録してみる

とりあえず、適当にイベント登録してみましょうか。

```
function AlertPage() {
  Analytics.record({
    name: 'show_home',
  })
```

およ！？なんかカウントし始まった。でもこれでいいのか？

![](/images/aws-amplify-analytics-01/2023-06-06-13-13-20.png)

適当にボタンを設置してボタンクリックイベントを取得してみましょう。

```
function AlertPage() {
  Analytics.record({
    name: 'show_home',
  })

  return (
    <Flex direction="column" width="100px">
      TestPage
      <Button
        variation="primary"
        onClick={() => {
          Analytics.record({
            name: 'click_detail',
          })
        }}
      >
        商品詳細
      </Button>
      <Button
        variation="primary"
        onClick={() => {
          Analytics.record({
            name: 'click_confirm',
          })
        }}
      >
        確認画面
      </Button>
      <Button
        variation="primary"
        onClick={() => {
          Analytics.record({
            name: 'click_billing',
          })
        }}
      >
        支払い
      </Button>
    </Flex>
  )
}
```

イベント数は増えているけど、イベント名が出てこない・・・
公式ページによると、最大72時間をようする場合があるとのことなので、すぐには出てこないのね。

> ※ 初回、「Enable Filters」ボタンを押下してからフィルターの機能が使用できるようになるまで數十分から１時間程度時間を要する場合があります。
> 過去に送信されたイベントのデータ量によっては、最大 72 時間を要する場合があります。

https://docs.aws.amazon.com/pinpoint/latest/userguide/analytics-events.html

![](/images/aws-amplify-analytics-01/2023-06-06-13-22-31.png)


## ファネル分析をやってみよう

とりあえず、待ってても仕方がないので次の「ファネル分析」とやらをやってみます。

![](/images/aws-amplify-analytics-01/2023-06-06-13-34-46.png)

うぉー！！ここでもイベント名のところで捕まった〜。
ひとまず諦めよう・・