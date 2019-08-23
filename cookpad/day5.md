# Day5

## MicroServicesArchitecher #33

- システムを分けていくことで組織を分けていく
    - 組織に合わせて分けるのとは逆の考え方

## Communication between services #53, 54

- ライブラリモデル
    - アプリケーションごとにライブラリを配置
- Service Meshモデル
    - proxyで集中管理

## Infrastructure as Code #65

- terraform
- Itamae

## Grafana #73

- 可視化ツール
    - Make dashboard
    - Many plugins

## Prometheus #79

- 動的なクラウド環境を構築するのに役立つ
- Alertmanagerで通知管理
    - Runbook: アラート対応手順書 を設定

###  運用

- Pull Request で設定を自動で走らせる

## コンテナオーケストレーション

- Docker(file)が普及したことで物理的にサーバを用意してそのサーバにパッケージをインストールするという作業が必要なくなった
    - サーバ上でDockerを動かすことができれば、開発者がDockerで動くアプリケーションをかければ問題ない
- コンテナが増えた場合、それをどのホストに配置するかが大変: コンテナオーケストレーションで解決
    - k8sが有名
    - AWSだとECSと**Fargate**がある
    - コンテナが死んだら他のホストに再配置、空いているホストにコンテナを配置

### k8s

#### メリット

- OSS
    - 改造することが可能

#### デメリット

- システムが複雑
    - 学習コストが高い
- エコシステムを構築しづらい
    - 間に抽象的なレイヤー(ex. [Hako](https://github.com/eagletmt/hako))を用意できない?

## Hako console

- AWS の各種リソースを視覚的に管理
- Dashboardにリンク
- Add users and teams

## Serverless

- サーバがないわけではなく、サーバの管理の必要がなくなる
- スケールに必要な条件が不明瞭なときに向いている(突然バズったり)
- [AWS serverless pattern](https://aws.amazon.com/jp/serverless/patterns/serverless-pattern/)
- AWS SAM: AWS公式のterraform?
    - Change setでリソースの変更ができる?

### イベントドリブンアーキテクチャ

- サーバレスを選択した際に、スケーリングや耐障害性を確保しやすい

## Auth

- ID Token
    - JWT(Json Web Signature)
        - ID Token
        - JWT(Json Web Token)

### Cookpad での採用例

1. (user -> ios-cookpad: Client) アクセス
2. (ios-cookpad -> auth-center) 認可リクエスト
3. (auth-center -> user) 許可リクエスト
4. (user -> auth-center) 許可する
5. (auth-center -> ios-cookpad) Send access token
6. (ios-cookpad -> pantry: Resource server) Access with access token
7. (pantry -> auth-center) Verify access token
8. (pantry -> ios-cookpad) Send data

- 複数のリソースサーバがある場合、アクセストークンをその分検証する必要がある
    - 解決策
        - Public Web API ではなく、認可サーバとクライアントが同社で作った場合、アクセストークンをキャッシュする
            - OAuth2 はクライアントを疑う仕組み

## DynamoDB

- User -> RequestRouter -> StrageNode
    - StargeNodeはそれぞれのAZのStrageNodeに非同期でコピーを作る: 可用性、スループットの改善
    - Put Item するときRequestRouterからStrageNodeに行く際どこかの3つのStrageNodeからLeaderを決めてそこに書き込む
        - 可用性の確保

### 分割

- Primarykey -> hash value
- ハッシュ値からテーブルを分割、分割したものをそれぞれのAZに配置
- pk, skと抽象的な列名にすることで、recipe\_id: xxx, user\_id: yyyということができる
