---
title: "【S3】クロスリージョンレプリケーションをするのに、バージョニングを有効にしないとできないらしいので実際にやってみた"
emoji: "💨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "S3", "SAA"]
published: true
---

## S3のクロスリージョンレプリケーション要件

バージョニングを有効にしないとレプリケーションの設定ができないと言うことなので、実際にやってみた。

![](/images/37adf2fbccb649/2021-09-23-10-27-23.png)

確かにできないね。



## 参考
[オブジェクトのレプリケーション](https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/replication.html#crr-scenario)