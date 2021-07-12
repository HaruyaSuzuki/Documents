# MySQLへ接続
mysql -u [user name] -p --host 127.0.0.1

# 一連の操作の流れ
## データベースの確認
> show databases;
## データベースへ接続
> use [データベース名];
## テーブル一覧を表示
> show tables;
## テーブルの構造確認
> desc [テーブル名];
## データの表示
> select * from [テーブル名];



# データベースの削除
## 通常
> drop database (if exists) [削除するデータベース];
## ハイフンを含んだデータベースを削除する
> drop database `[ハイフンの含んだデータベース名]`;

# MySQLの初期化
## プロセスが起動しているか確認
> ps -efw | grep -i mysql
## 通常のサービス停止
- サービスの停止
> /etc/init.d/mysql stop
- サービスの停止ができなかった場合
> killall mysql
- 既存のデータフォルダを気休めバックアップ
> cd /var/lib
> cp -arf mysql/mysql_backup/
- mysql/ の中身を削除
> cd /var/lib/mysql;
> rm -rf *
- MySQLの初期化
> su - mysql

# テーブルの削除
> drop table [テーブル名];

## 汎用的なデータベースの削除
- 削除するディレクトリの確認。
> show variables like 'datadir';
> sudo rm -r [mysqlディレクトリまでのパス]/mysql/*
- mysqlユーザになる
> sudo su - mysql
- データベース初期化
> mysql_install_db --datadir=/opt/vcs/mysql -user=mysql