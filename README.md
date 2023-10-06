# Docker DesktopでECSにコンテナを構成する

Docker DesktopでECSにコンテナを構成する。

## 環境構築

1. 環境変数
  `.env`ファイルに以下の要素を指定
    | 変数名 | 指定内容 |
    |--------|----------|
    | `AWS_VPC_ID` | VPCのID |
    | `AWS_ACCOUNT_ID` | アカウントID |
    | `AWS_REGION` | リージョン名(例: `ap-northeast-1`) |
    | `IMAGE_NAME` | ECRに登録したレポジトリ名 |
    | `IMAGE_URI` | イメージのURI(通常は`AWS_ACCOUNT_ID`，`AWS_REGION`，`IMAGE_NAME`で生成する) |
1. ビルド
  `docker compose build`
1. プッシュ
  `docker push ${IMAGE_URI}`


## コンテナの起動と実行

1. コンテキストを切り替える
    `docker context use ecs-context`

1. コンテナを起動する
    `docker compose up -d`


## 注意

- 予め`aws`コマンドでAWSへログインできる状態にしておく
  (`profile`，`credential`が正しく設定されている)
- `docker login`する
  ECRのレポジトリ管理画面にプッシュ方法が書いてあるので参考にする。
  ```
  aws ecr get-login-password \
    --region "${AWS_REGION}" \
  | docker login \
    --username AWS \
    --password-stdin \
    "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
  ```
