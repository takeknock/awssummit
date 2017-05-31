# Sansan
## 困った話、それをメッセージングで解決した話
## 講演者
- 神原(@atsukanrock)
- 40人チームのマネジメント
- 興味
    - Domain-Driven Dev
    - C#
    - Enterprise Integration Pattern

## Sansanのサービスについて
- 企業向け名刺管理アプリ：sansan
- 個人向け：エイト

### Sansan
- 企業ごとにかき集める(外交記録)
- サービス規模の拡大→すけーらびりてぃの課題が次々に発生

## メッセージングとは
- メッセージキューを介し、プロセス間やアプリケーション
- 処理するやつ：consumer

### 特徴
- メッセージは単なるテキスト

- Transaction: ACID特性を満たさない
- At-most-once: 対応しないことですけーらびりてぃ確保

- c.f.
    - ACID特性

# 課題1
- 巨大なトランザクション：
    - 法人向け名刺管理：大きな企業でも1つのDBで管理。
    - 見れたり見れなかったり権限設定したい
        - もしRDBでやると、from×toのレコード数が必要
    - 5000×5000をRDBで1トランザクションでInsertする→無理→メッセージングへ
## 実装例
- User→(洗い替え処理)→webserver(POST等の1トランザクションで終わらない)→Amazon SQS Queue A→consumer(5000個のメッセージへ分割)→Amazon SQS Queue B→Consumers(分散処理)→Database

# 課題2
- 終わらないバッチ処理
    - Non-scalable Design
    - データ化したものへ処理を加える(バッチのイメージ)
- 解決方法
    - 1件処理終わったら、すぐに後続処理を起動
- c.f.
    - Domain Eventとは
    - not DE: Aは次にBなことを知っている
    - DE : Event Aggregatorを用意。(Domain Driven Designで提唱)Aは終わったら、EventAggregatorへ通知。その終わりを知りたい処理は、EventAggregatorを購読しておく。
## 実装例
- publisher(終わりましたよ通知)→Amazon SNS Topic(カブサブモデル実装のために使われるサービス。EventAggregatorとして使う)→Amazon SQS Subscriber A and B→consumer(後続処理)

# 課題3
- 急激に変化するデータベース負荷
    - Digitization Throughput(日中に10万件とかだが、夜中は1万件以下)
    - データベース負荷を安定させたい
    - 平均値を超える部分については、空いている時間に処理できるようにすれば、負荷を馴らすことができる
## 実装例
- Digitization Service→Web API Server→Amazon SQS Queue→Consumer→

- c.f.
    - 並列度の制御
        - Autoscaling
        - SepahoSlimクラスで、スレッド並列度を制御
# 低いメンテナンス自由度
- 別チームとの連携。メンテナンスの際止める必要
## 実装例
- SQS Queueにためるようにする。メンテナンスが終わったら、consumerに投げるようにする。


# 注意点
- アプリケーション側で、冪等性を保証する必要がある
    - c.f.冪等性:ある操作を何回行ったとしても結果が同じこと。REST API設計(HTTP POST冪等性ない)とHTTP PUT(冪等性あり)
    - インフラ環境: Chef、Ansibleは設定を何度実行しても同じ処理がされる

- 強い一貫性モデル(ACID)を持つRDB等で保障するのが基本←ここがスケーラビリティのボトルネックになる。ここの設計が難しい

- 順序は保証されない
    - 順序保証は自前で行う必要がある。FIFO Queueであれば、順序保証。(TKY Region未対応)

- 結果整合性モデルになる例

# メッセージング
- MERIT
    - スケーラビリティ
    - 県労政
    - 運用性
- DEMERIT
    - 設計の複雑性があがる。
