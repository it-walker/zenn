---
title: "定番中の定番[TDDハンズオン]をやってみた"
emoji: "📘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["typescript", "jest", "tdd"]
published: true
---

## はじめに

TDDのハンズオンとして、有名な`FizzBuzz`のハンズオンをやってみたいと思います。
下記の、テストを実際にやっていきます。

1. 実装されている
2. 引数にとった値を文字列で返す
3. ただし、3の倍数の時は「Fizz」を返す
4. ただし、5の倍数の時は「Buzz」を返す
5. ただし、3と5の両方の倍数の場合には「FizzBuzz」を返す
6. 引数が1から100までの数でない場合は例外にする。

## 1. 実装されている

失敗するテストコードを書いていきます。まだ実装されていないので、当然ながらエラーとなります。

```
describe('FizzBuzzTest', () => {
  it('Test実装されている', () => {
    FizzBuzz(1)
  })
})
```

テスト実行すると、期待通りエラーとなります。

まだ実装すらしていないので、ここでとりあえず`FizzBuzz()`を作り、テストを成功させます。

```fizzbuzz.ts
export function FizzBuzz(num: number) {
  // まだ何も実装していない
}

export default FizzBuzz
```

とりあえず`FizzBuzz()`を作成したことでテストが成功しました。

```
 PASS  tests/fizzbuzz.test.ts
  FizzBuzzTest
    ✓ Test実装されている (1 ms)


> Test run finished at 2023/4/8 18:34:54 <

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.275 s
```

![](/images/tdd-study-handson/2023-04-08-18-40-13.png)

## 2. 引数にとった値を文字列で返す

次に、引数にとった値を文字列で返すテストコードを書いていきます。
まだ`FizzBuzz()`は何も返さないので、これでテストが失敗します。

```fizzbuzz.test.ts
it('引数にとった値を文字列で返す', () => {
  expect(FizzBuzz(1)).toEqual('1')
})
```

```
 FAIL  tests/fizzbuzz.test.ts
  FizzBuzzTest
    ✓ Test実装されている (1 ms)
    ✕ 引数にとった値を文字列で返す (3 ms)

  ● FizzBuzzTest › 引数にとった値を文字列で返す

    expect(received).toEqual(expected) // deep equality

    Expected: "1"
    Received: undefined

      16 |
      17 |   it('引数にとった値を文字列で返す', () => {
    > 18 |     expect(FizzBuzz(1)).toEqual('1')
         |                         ^
      19 |   })
      20 | })

      at Object.<anonymous> (tests/fizzbuzz.test.ts:18:25)

Test Suites: 1 failed, 1 total
Tests:       1 failed, 1 passed, 2 total
Snapshots:   0 total
Time:        0.27 s, estimated 1 s
Ran all test suites related to changed files.
```


![](/images/tdd-study-handson/2023-04-08-18-40-47.png)


```fizzbuzz.ts
export function FizzBuzz(num: number): string {
  return num.toString()
}

export default FizzBuzz
```


予定通り、テストが成功しました。

```
 PASS  tests/fizzbuzz.test.ts
  FizzBuzzTest
    ✓ Test実装されている
    ✓ 引数にとった値を文字列で返す (1 ms)


> Test run finished at 2023/4/8 18:42:02 <

Test Suites: 1 passed, 1 total
Tests:       2 passed, 2 total
Snapshots:   0 total
Time:        0.215 s, estimated 1 s
Ran all test suites related to changed files.
```

![](/images/tdd-study-handson/2023-04-08-18-42-53.png)

## 3. ただし、3の倍数の時は「Fizz」を返す

3の倍数ね。まずテストコードを作成します。

```fizzbuzz.test.ts
it('ただし、3の倍数の時は「Fizz」を返す', () => {
  expect(FizzBuzz(3)).toEqual('Fizz')
})
```

まだ実装していないので、テストは失敗します。

```
 FAIL  tests/fizzbuzz.test.ts
  FizzBuzzTest
    ✓ Test実装されている (1 ms)
    ✓ 引数にとった値を文字列で返す (2 ms)
    ✕ ただし、3の倍数の時は「Fizz」を返す (4 ms)

  ● FizzBuzzTest › ただし、3の倍数の時は「Fizz」を返す

    expect(received).toEqual(expected) // deep equality

    Expected: "Fizz"
    Received: "3"

      20 |
      21 |   it('ただし、3の倍数の時は「Fizz」を返す', () => {
    > 22 |     expect(FizzBuzz(3)).toEqual('Fizz')
         |                         ^
      23 |   })
      24 | })

      at Object.<anonymous> (tests/fizzbuzz.test.ts:22:25)


> Test run finished at 2023/4/8 18:44:04 <

Test Suites: 1 failed, 1 total
Tests:       1 failed, 2 passed, 3 total
Snapshots:   0 total
Time:        0.267 s, estimated 1 s
Ran all test suites related to changed files.
```

テストが予定通り失敗したので、実装を直していきます。

```diff ts
// 修正前
export function FizzBuzz(num: number): string {
-  return num.toString()
}
---
// 修正後
export function FizzBuzz(num: number): string {
+   if (num % 3 === 0) {
+     return 'Fizz'
+   }
  return num.toString()
}
```

これでテストが成功しました！

![](/images/tdd-study-handson/2023-04-08-18-52-59.png)

## 3. ただし、5の倍数の時は「Buzz」を返す

同様にテストから作成していきます。

```
it('ただし、5の倍数の時は「Buzz」を返す', () => {
  expect(FizzBuzz(5)).toEqual('Buzz')
})
```

はい、これで予定通りテストが失敗したので、実装を修正していきましょう。

![](/images/tdd-study-handson/2023-04-08-18-54-55.png)

```diff ts
// 修正前
export function FizzBuzz(num: number): string {
  if (num % 3 === 0) {
    return 'Fizz'
  }
  return num.toString()
}
---
// 修正後
export function FizzBuzz(num: number): string {
  if (num % 3 === 0) {
    return 'Fizz'
  }
+  if (num % 5 === 0) {
+    return 'Buzz'
+  }
  return num.toString()
}
```

はい、これでテスト成功まで辿り着けました。

![](/images/tdd-study-handson/2023-04-08-18-57-10.png)


## 4. ただし、3と5の両方の倍数の場合には「FizzBuzz」を返す

3と5の倍数なので、`15`を渡したときに`FizzBuzz`が返ってくる想定のテストコードを作成します。

```
it('ただし、3と5の両方の倍数の場合には「FizzBuzz」を返す', () => {
  expect(FizzBuzz(15)).toEqual('FizzBuzz')
})
```

予定通りテストが失敗したので、次に実装を修正します。

![](/images/tdd-study-handson/2023-04-08-19-12-15.png)


```diff ts
// 修正前
export function FizzBuzz(num: number): string {
  if (num % 3 === 0) {
    return 'Fizz'
  }
  if (num % 5 === 0) {
    return 'Buzz'
  }
  return num.toString()
}
---
// 修正後
export function FizzBuzz(num: number): string {
+  if (num % 3 === 0 && num % 5 === 0) {
+    return 'FizzBuzz'
+  }
  if (num % 3 === 0) {
    return 'Fizz'
  }
  if (num % 5 === 0) {
    return 'Buzz'
  }
  return num.toString()
}
```

これでテストが成功！

![](/images/tdd-study-handson/2023-04-08-19-15-26.png)


## 5. 引数が1から100までの数でない場合は例外にする

まずテストを作成します。

```
it('引数が1から100までの数でない場合は例外にする。', () => {
  expect(() => FizzBuzz(101)).toThrow('Error!')
})
```

よし、予定通りテスト失敗しました。
実装を修正していきます。

![](/images/tdd-study-handson/2023-04-08-19-26-40.png)


```diff ts
export function FizzBuzz(num: number): string {
  if (num % 3 === 0 && num % 5 === 0) {
    return 'FizzBuzz'
  }
  if (num % 3 === 0) {
    return 'Fizz'
  }
  if (num % 5 === 0) {
    return 'Buzz'
  }
  return num.toString()
}
---
export function FizzBuzz(num: number): string {
+  if (num < 1 || 100 < num) {
+    throw new Error('Error!')
+  }
  if (num % 3 === 0 && num % 5 === 0) {
    return 'FizzBuzz'
  }
  if (num % 3 === 0) {
    return 'Fizz'
  }
  if (num % 5 === 0) {
    return 'Buzz'
  }
  return num.toString()
}
```

テストに成功しました。

![](/images/tdd-study-handson/2023-04-08-19-28-29.png)


これで、全てのテストが成功することになりました。

![](/images/tdd-study-handson/2023-04-08-19-29-30.png)


## 参考リンク

https://tech.uzabase.com/entry/2021/03/17/165008