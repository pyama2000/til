# Redis

## Redisとは

キーと5種類のデータ型の対応関係を格納する非常に高速な非リレーショナルデータベース

## データ型

- String
    - key / value
    - key-valueのセットを複数持つイメージ
- List
    - key: List名 / value: Listに格納する値
    - Listの先頭か末尾にvalueを追加する
    - List自体を複数持つイメージ
- Set
    - key: Set名 / value: Setに格納する値
    - 重複を許さない
    - 順不同
    - Set自体を複数持つイメージ
- Sorted Set
    - key: Set名 / value: Setに格納する値
    - 重複を許さない
    - 順番はscoreで保存する(Setへの保存時にscoreを指定)
    - sorted Set自体を複数持つイメージ
- Hash
    - key: Hash名 / value: fieldとvalueを持つHash
    - HashMap<String, String>の入れ子構造
    - 順不同
    - Hash自体を複数持つイメージ

## Redisの使い所

- 有効期限のあるデータを扱う場合
    - セッション、ワンタイムトークンなど
    - データ保存時にexpire指定できる
- ランキングデータを扱う場合
    - Sorted Set(ユーザID/スコアなど)を利用する
    - RDBの`ORDERD BY`より速い
- IoTデータの一時保存先として使う場合
- Pub/Subを使う場合

## 参考

> [Redisの特徴について容易にまとめてみた](https://qiita.com/tomu28/items/8f13145bd8d45523a195)
> [RedisとElastiCacheを分かりやすくまとめてみた](https://qiita.com/gold-kou/items/966d9a0332f4e110c4f8)
> [webエンジニアのためのはじめてのredis](https://www.slideshare.net/ssusera66c10/webredis)
