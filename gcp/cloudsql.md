# Cloud SQL

## Cloud SQLの設定
- Cloud SQL Admin API を有効化
GCPサイト上からAPIを有効化する。
- gcloud にログイン
```
gcloud auth application-default login
```
- Cloud SQL ローカルの有効化
```
gcloud services enable sqladmin
```
- Cloud SQL Proxy のインストール
```
curl -o cloud_sql_proxy https://dl.google.com/cloudsql/cloud_sql_proxy.darwin.amd64
```
- Cloud SQL Proxy の権限変更
```
chmod +x cloud_sql_proxy
```
- Cloud SQL インスタンスの作成
GCPサイト上からCloud SQL - インスタンスを作成する。
- ユーザーの作成
GCPサイト上のSQL - ユーザから作成。
- データベースの作成
GCPサイト上のSQL - データベースから作成。
- データベースの準備
settings.pyにてDATABASEの設定&secret.yaml, secret_dev.yamlの設定を行う。
- Homebrewのインストール
```
brew install mysql
```
- mysqlclientのインストール
```
pip install mysqlclient
```
- Cloud SQL インスタンスの初期化
```
./cloud_sql_proxy -instances=[YOUR_INSTANCE_CONNECTION_NAME]=tcp:3306
```
## MySQLの初期化
- GCPのデータベースから登録したDBを削除する。
- 新しくデータベースを作成すれば完了。
## MySQLの操作
Ready for conectionを行なっている状態で下記コマンド。
```
mysql -u [user name] -p --host 127.0.0.1
```