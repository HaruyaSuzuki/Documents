# GCPへのデプロイ

> AppEngine設定
  GCPサイト上からAppEngineに移動し、プロジェクトを作成。

> app.yamlファイル作成
  プロジェクトにて app.yaml ファイルを作成、設定し、gunicornなどのモジュールをインストールする。

> gcloudにログイン
  ターミナルで gcloud auth login を実行。

> プロジェクトの選択
  ターミナルで gcloud config set project PROJECT_ID を実行。

> 現在選択しているプロジェクトの確認
  ターミナルで gcloud init を実行。
  現在のプロジェクト名などが確認できる。(確認できたらCtrl+cで中止)

> デプロイするプロジェクトを指定して実行(デプロイ)
  ターミナルで gcloud app deploy --project PROJECT_ID を実行。