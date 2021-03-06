# AWS Well-Architected Frameworkによる
## 講演者
畑史彦

## コンテンツ
- 紹介
- クラウドでのアプリケーション設計の考え方
- クラウドでのアプリケーション設計のケーススタディ

# Well hogeの考え方
- 使い方や疑問
- 様々なリソースやサポートがある
   - ドキュメントやユーザコミュニティ
- 使い方は上記わかってもどう組み合わせて設計すればよいか？
- そこでAWS Well-Architected Framework(WAF)ですよ
  - 考え方とベストプラクティス
  - アーキテクチャを評価するための一貫したアプローチとしても使える


# WAF構成要素
## 5つの柱
- セキュリティ
- 信頼性
- パフォーマンス効率
- コスト最適化
- 運用性

## 設計原則(5つの柱のベース)
- 個別具体についてはWeb上にある
- より汎用的な原則として提示している
- 一般的な設計原則と各柱ごとの設計原則

## 質問事項
- 質問に従って自問することでシステムをレビューすることができる
- 忘れられがちな基本的領域にも対応

# クラウドでのアプリケーション設計の考え方
- 全体は紹介できないので、1つピックアップして紹介
## あらゆるシステムコンポーネントはダウンする
- 個々のコンポーネントがダウンしても、
  - 自動で検知
  - 復旧
  - アーキテクチャ全体が落ち

- 障害を未然に防止しようとするのではなく、

### MTTF and MTTR
- Availability = MTTF / (MTTF(平均故障時間) + MTTR(平均修復時間))

### Not only Availability...
- テストとテスト作成を自動化


# 具体的にどういう構成ができるのか
- Automatic Feedback control
  - トレーサビリティの設計原則
  - サーバーレス(パフォーマンス最適化)
- Continuous Delivery & Test Automation
  1. 問題が起きないように時間をあけて慎重に開発、テスト、デプロイを実施する
    - 問題が発生しても、修正、テスト、デプロイが即座に可能な買いは宇tプロセスを整備する
  1. ばぐぉ出さないように大量の単体テスト
    - テストを自動生成

- Continuous Delivery
  - コード変更が発生すると、自動的にビルド、テスト、および本番へのdプロ委準備が実行される開発手法
  - デプロイ準備の整ったビルドの青果物をもとに
- Property Based testing←→example based testing
  - 定義された質を満たすかを検証するために、大量のテストを

## AWS CodePipeline:
- 継続的デリバリーサービス

## AWS CodeBuild
## AWS CodeDeploy

バグを発見したらこのプロセスをまとめて

### 採用原則
- 一般的な」設計原則
  - アーキテクチャの実験を容易にするために自動化を取り入れる
- 運用性の設計原則
- コスト最適化の設計原則

# 本番を想定したテスト(game-day Testing)
- game-day: 試合がある日の
- トラブルが起きた時しかトラブルシュートしなくて、いざトラブルが起きたときにスムーズに対応ｄけいますか？
- 実際の本番環境で、異常事態の対応を訓練
- 数人のチームで対応するコンテストも実施してる

本番と同様の環境を用意するためのサービスがある。AWS CloudFoundation

### AWS CloudFoundation
テンプレートをもとに、関連する一連のAWSリソースのプロビジョニングが可能。
