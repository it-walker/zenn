---
title: "[Amplify×figma]コンポーネント化した部品から、さらにコンポーネントを作成してみるも、あえなく撃沈した話"
emoji: "🦁"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["amplify", "figma"]
published: true
---

## チェックボックスのデザインをデフォルトでどこまで変えられるのか

チェックボックスのデザインを変えたいと思ったとき、どこまで変えられるのでしょうか。
今のところ、`AWS Amplify UI Kit`で用意されているプリミティブなコンポーネントは、デザインに制約があって、その中でやる分にはいいのですが見た目をもう少し凝りたいときはそう簡単ではないことは分かっています。
もう少しどうにかなんないの？をやっていきたいと思います。

## チェックボックスのアイコンの色・形を変えたい

というわけで、まずは色と角丸を変えてみたいのです。
実装上に変更するのはできます。できるのですがデザインの世界はできるだけデザインの世界で完結させたいんですよね。
デザインのことは全てfigma側だけでどうにかできないか。

![](/images/amplify-figma-study-02/2023-04-15-10-59-38.png)

デフォルトで用意されている`CheckboxField`にある`Icon`の角の半径をいじって丸くしてみました。
同様に`Icon`の色を緑色にしてみます。

![](/images/amplify-figma-study-02/2023-04-15-11-01-50.png)

![](/images/amplify-figma-study-02/2023-04-15-11-03-38.png)

![](/images/amplify-figma-study-02/2023-04-15-11-06-31.png)

`Amplify Studio`に取り込んでみると、プレビュー画面上は下記のようになります。
見事に設定が無視されています。

![](/images/amplify-figma-study-02/2023-04-15-11-07-30.png)

`Icon`は🔒がついているので、読み取り専用？というか設定は無視されてしまうようですね。
なので、figmaでいくら設定を変更してもダメみたいです。

## チェックボックスとラベルが連動するようにしたい

チェックボックスのON/OFFでラベルを変更させたいです。
とりあえず、既存に備わっているチェックボックス（`CheckboxField`）とバッジ（`Badge`）を組み合わせてみます。

![](/images/amplify-figma-study-02/2023-04-15-14-44-21.png)

## バリアントを作成して、ON/OFF時のレイアウトを作成する
figma上でONとOFFのときのレイアウトを作成してみます。
バリアントを追加して、ON時のレイアウト、OFF時のレイアウトを作成すればいけそうですね。
`checked=on`、`checked=off`を作成して`Badge`インスタンスの属性で、`variation=success`、`variation=error`を使用します。
まずはあるものをうまく使ってやる方向で行きます。

figmaの出来上がりはこんな感じ。

![](/images/amplify-figma-study-02/2023-04-15-14-56-30.png)

では取り込んで画面表示してみましょう！

![](/images/amplify-figma-study-02/2023-04-15-15-56-50.png)

よしよしうまく行った！
チェックのON/OFFを切り替えてみます。

![](/images/amplify-figma-study-02/2023-04-15-15-57-20.png)

`MyCheckbox`の実装部分のサンプルです。
レイアウト部分は一切手を入れずに、動きの部分だけ実装しています。
色味については、もともと用意されているテーマに任せています。

```tsx MyCheckboxWrapper.tsx
const MyCheckboxWrapper = (props: MyCheckboxProps) => {
  const [myCheckbox, setMyCheckbox] = useState<MyCheckboxProps>({
    checked: props.checked ?? 'off',
  });

  return (
    <>
      <MyCheckbox
        checked={myCheckbox.checked}
        overrides={{
          CheckboxField: {
            defaultChecked: (myCheckbox.checked === 'on'),
            testId: "myCheckbox",
            value: "1",
            onClick: () => {
              const prop = { ...myCheckbox }
              if (myCheckbox.checked === 'off') {
                prop.checked = 'on'
              } else {
                prop.checked = 'off'
              }
              setMyCheckbox(prop)
            }
            },
        }}
      />
    </>
  )
}

export default MyCheckboxWrapper
```


## 作成したコンポーネントを使って、もう少し大きなコンポーネントを作成する
画面を作っていくと、1つ1つの部品もさることながら、もう少し大きな単位でコンポーネントを作成するケースもあると思います。
先ほど作ったチェックボックスのコンポーネントで、さらにそのチェックボックスを配置した部品を作ってみます。

イメージはこんな感じ。
この後いろいろ調整していきます。

![](/images/amplify-figma-study-02/2023-04-15-16-22-06.png)

## オートレイアウトを使って並びをキレイにする

今回は単純に縦に並べるのと、「〜に同意する」とチェックボックスをワンセットで、空きをそれぞれ調整したいので、フレームを２階層にします。
最終系はこんな感じ。

![](/images/amplify-figma-study-02/2023-04-15-16-31-01.png)

え？なんでや？チェックボックスのテキスト部分が反映されない。

![](/images/amplify-figma-study-02/2023-04-15-16-35-55.png)

今のろころ解決策ないので、オーバーライドすることで回避します。

```tsx
/**
 * overridesは、インスタンスの階層になっているので、
 * MyAgreement>MyCheckbox1、MyAgreement>MyCheckbox2のlabelを
 * 実装側で設定すれば画面表示で切り替えられます。
 */
export const MyAggrementWrapper = (props: MyAgreementProps) => {
  return (
    <>
      <MyAgreement
        overrides={{
          MyCheckbox1: {
            overrides: {
              CheckboxField: {
                label: '同意する',
              }
            }
          },
          MyCheckbox2: {
            overrides: {
              CheckboxField: {
                label: '同意する',
              }
            }
          }
        }}
      />
    </>
  )
}
```

これで回避できるやろと思っていたらダメでした。。
今時点で自分が理解できていないのかもしれないですが、現状の理解は下記の通り。

本当は動きをつけた`〜Wrapper.tsx`をコンポーネントとして使用したかったのですが、
実装側で作ってしまっているのでfigmaとうまく連動することができない。
→もしやるなら、動きの実装をさらに作成することになるので、コンポーネント側で隠蔽することができない。。

えー、そうなのー？😱
うーん、今日はひとまずここまでにしよう。。

![](/images/amplify-figma-study-02/2023-04-15-17-04-31.png)