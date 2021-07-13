# MySQL

## MySQLへ接続
```
	mysql -u [user name] -p --host 127.0.0.1
```

## 一連の操作の流れ
- データベースの確認
```
	show databases;
```
- データベースへ接続
```
	use [データベース名];
```
- テーブル一覧を表示
```
	show tables;
```
- テーブルの構造確認
```
	desc [テーブル名];
```
- データの表示
```
	select * from [テーブル名];
```


## データベースの削除
- 通常
```
	drop database (if exists) [削除するデータベース];
```
- ハイフンを含んだデータベースを削除する
```
	drop database `[ハイフンの含んだデータベース名]`;
```

## テーブルの削除
```
	drop table [テーブル名];
```