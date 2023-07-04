---
title: "手っ取り早くテストを作れちゃう！cypressの`experimentalStudio`"
emoji: "🎉"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Cypress", "e2e", "test"]
published: true
---

e2eテストでお馴染みの、`Cypress`を最近使っています。
最初は慣れるまでテストコードを書くのがしんどくないですか？
ある程度慣れてくればささっと描けるようにはなるのかもしれませんが、なかなかに苦戦する人も多いのではないでしょうか？

今回は、Cypressについて、いろいろと触ってきてわかったことがあったので、それを共有したいと思います。

## ちょっと確認したい時は、`experimentalStudio`を使うと楽ちん！

なんと、`experimentalStudio`という設定を追加するだけで、テストの操作を直接実施するだけで、テストコードを自動で出力してくれるんです！！
めちゃめちゃ夢広がる！

## きっかけ
さてさて、Cypressの使い方として合っているかは難しいところですが、GA4を使って、どういう情報を入力したとか、どのボタンをクリックして次の画面へ遷移したのかなどの情報を集計したいという要件が発生しました。
GA4のことについては割愛しますが、そんなときに、ちゃんと集計できているかどうかを確認するために、何種類かの想定で、実際に画面を操作したり、入力したりと、全てのパターンを毎回人力で入力するようなことをしていました。
いやーこれがまた面倒で面倒で・・
めんどくさいなら、楽をしようということで、`Cypress`でマクロ的な使い方をしてしまおうというわけです。

## 具体例

では、実際になにをすればいいかを書いていきましょう。
`cypress.config.ts`に`experimentalStudio`の設定を追加するだけ。

```diff cypress.config.js
import { defineConfig } from "cypress";

export default defineConfig({
  e2e: {
+   experimentalStudio: true,
    setupNodeEvents(on, config) {
      // implement node event listeners here
    },
  },
});
```

これで`Cypress`を起動してみます。
すると、下記のように、テストの追加が画面上でできるようになっています。

![](/images/cypress-experimental-studio/2023-07-04-18-51-42.png)

`Query`というリンクをクリックしてみます。

![](/images/cypress-experimental-studio/2023-07-04-18-57-31.png)

続けて、`Button`をクリックしてみましょうか。

![](/images/cypress-experimental-studio/2023-07-04-18-58-51.png)

`Save Commands`をクリックしてみましょう。

![](/images/cypress-experimental-studio/2023-07-04-18-59-33.png)


これだけで、操作した部分をテストとして実装してくれました。
マクロみたいですよね！？

![](/images/cypress-experimental-studio/2023-07-04-19-00-40.png)


実際にテストコードはどうなっているかというと、、
下記のようになっています。
`/* ==== Generated with Cypress Studio ==== */`〜`/* ==== End Cypress Studio ==== */`で囲まれているところが自動で追加されたところのようです。
しっかり分かるようにしてくれている！親切！！


```diff spec.cy.js
describe('template spec', () => {
  it('passes', () => {
    cy.visit('https://example.cypress.io')
+   /* ==== Generated with Cypress Studio ==== */
+   cy.get(':nth-child(4) > .row > .col-xs-12 > .home-list > :nth-child(1) > ul > :nth-child(2)').click();
+   cy.get(':nth-child(4) > .row > .col-xs-12 > .home-list > :nth-child(1) > :nth-child(1)').click();
+   cy.get('#query-btn').click();
+   /* ==== End Cypress Studio ==== */
  })
})
```

## ポイント

というわけで、総括すると、

cypress.config.js(ts)に、`experimentalStudio: true`を追加してあげると、画面上で操作したことを記録してくれます。
まるでExcelのマクロ機能のようですよね！？

まずはささっとやりたいテストの操作を行い、自動出力してくれたコードを修正するもよし、テストと割り切って自動で出力してくれたままでもよし、ですよね。

今回は、GA4を計測するための何パターンかの操作が必要だったので、作りはどうでも良くささっと短時間で作れるものが欲しかった。
そういった用途であれば、この機能、だいぶいいぞ。
今後も活用していきたいと思います。

