## 講演者
滝沢与一

## 環境
1. 金融機関における、ビジネスモデルの変革の必要性
1. FinTech
1. 銀行API
1. FISCガイドライン

### ビジネスモデルの転換を求める金融行政
- 「平成28年事務年度　金融行政方針」
- ガイドラインはクラウドを前提としたものへ
    - FISCガイドライン
        - 安全対策基準題8版追補改訂
        - システム監査方針
- 保障型監査の報告書を利用することが望ましい(AWSの出してるようなもの)

# FISC対応
- 対応のリファレンスをサポートするベンダーが出てきてる
    - NRI、TIS等

# 金融機関で求められるシステム要件
- 新しいIT環境の実現
- API
    - トランザクションをコントロールする仕組み(AmazonAPIGatewayであればスロットリング機能で実現可能)
    - 回復性
    - APIライフサイクル
    - SDKの世代
    - API動作のモニタリング
    - AWS認証
## HPC
- Amazon EC2 P2 インスタンス(GPUインスタンス:K80)
- 自動的に新しいデバイスを適用

## 可用性
- 自動化による、障害発生時の対応・体制の簡略化
- 自動で対処される←設計されているといえる←障害とは言わないで済む

- 原因分析といったところへコストを割く必要がなくなる。

- CloudWatchによる、設定監視

- Amazon Inspectorで、評価レポートを作成
    - エグゼクティブサマリーや評価詳細を含んだ評価レポート
    - 管理コンソールやAPI

# USの例
- Service Oriented Architectureの時間軸、キーとなるアクション
    - プロジェクトフェーズ：一部の人だけが使う
    - 初期フェーズ：チームができてくる
    - 移行フェーズ：プロジェクト増えるとID管理やトレーニング、専用線での接続等が必要になる。
    - 最適化：より変わっている状態にあったものへ変更
## Security by design（セキュリティを設計時に組み込む）
- あらかじめ監査の要件を含めてやっていく
    - オンプレミスだとつらい作業
    - AWSでは、すぐに使わなくても使えるよう準備だけして、設計しておいたほうがよい。
- キーワード：自動化
    - 手作業が入ると、リスク。
## AWSプロフェッショナルサービス for FinServ
- 決まった時間内に対応すると決まっている契約をする。

# AWS採用のクラウドジャーニー
# TCO分析の進め方
- 全体のシステムで分析。人件費とか含めたものをしてみたらよい。
