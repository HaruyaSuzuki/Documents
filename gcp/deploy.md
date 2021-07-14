# GCPへのデプロイ

- AppEngine設定
GCPサイト上からAppEngineに移動し、プロジェクトを作成。

- app.yamlファイル作成
プロジェクトにて app.yaml ファイルを作成、設定し、gunicornなどのモジュールをインストールする。

- gcloudにログイン
```
  gcloud auth login
```

- プロジェクトの選択
```
  gcloud config set project PROJECT_ID
```

- デプロイするプロジェクトを指定して実行(デプロイ)
```
  cloud app deploy --project PROJECT_ID
```