# MySQLで文字コードを変更する方法

## 文字コードの確認

### データベースやシステムの文字コードを確認

MySQLのシステム変数からMySQLの文字コードを確認する。

```mysql
mysql> SHOW VARIABLES LIKE 'char%';
+--------------------------+------------------------------------------------------+
| Variable_name            | Value                                                |
+--------------------------+------------------------------------------------------+
| character_set_client     | utf8                                                 |
| character_set_connection | utf8                                                 |
| character_set_database   | utf8                                                 |
| character_set_filesystem | binary                                               |
| character_set_results    | utf8                                                 |
| character_set_server     | utf8                                                 |
| character_set_system     | utf8                                                 |
| character_sets_dir       | /usr/local/Cellar/mysql/5.7.19/share/mysql/charsets/ |
+--------------------------+------------------------------------------------------+
```

- character\_set\_client: クライアント側で発行したSQL文の文字コード
- character\_set\_connection: クライアントから受け取った文字の文字コード
- character\_set\_database: 現在参照しているデータベースの文字コード
- character\_set\_results: クライアントに送る結果の文字コード
- character\_set\_server: データベース作成時の文字コード
- character\_set\_system: システムが使用する文字コード

以下のコマンドでも確認可能。

```mysql
mysql> status;
```

### テーブルの文字コードを確認

```mysql
mysql> SHOW CREATE TABLE <table_name>;
```

## 文字コードをUTF8に変更

### 設定ファイルを使用する方法

文字コードの変更を設定ファイルを使って変更する。

```/etc/my.cnf
[mysqld]
character-set-server=utf8

[client]
default-character-set=utf8
```

以下のコマンドで再起動を行う。

```bash
/etc/init.d/mysqld restart
```

### コマンドから変更する方法

データベースやシステムの文字コードは`SET`コマンドを用いて変更可能。

```mysql
mysql> SET character_set_database=utf8;
mysql> SET character_set_server=utf8;
```

ただし、既に作成したデータベース内の情報には変更が反映されないため以下のコマンドを実行する必要がある。

```mysql
# テーブルのデフォルトの文字コードを変更
mysql> ALTER TABLE <table_name> CHARSET=utf8;
# テーブルとカラムの文字コードを変更する場合は以下のコマンド
mysql> ALTER TABLE <table_name> CONVERT TO CHARACTER SET utf8;
# カラムの文字コードを1つずつ変更する場合は以下のコマンド
mysql> ALTER TABLE <table_name> MODIFY <column_name> <data_type> CHARACTER SET utf8 COLLATE utf8_general_ci;
```
