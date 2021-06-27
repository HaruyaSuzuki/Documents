# GAEへデプロイ
gcloud app deploy --project myportfoliosite-haruyasuzuki
# Cloud SQL へ接続
./secrets/cloud_sql_proxy -instances=[YOUR_INSTANCE_CONNECTION_NAME]=tcp:3306
# 静的ファイルの収集
python3 manage.py collectstatic
# version down
  gcloud components update --version 344.0.0