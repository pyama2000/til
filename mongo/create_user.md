# MongoDBでのユーザ追加方法

```
# mongo
> use admin
switched to db admin
> db.auth("USERNAME", "PASSWORD")
1
> use DATABASE_NAME
switched to db DATABASE_NAME
> db.createUser(
    {
      user: "USERNAME",
      pwd: "PASSWORD",
      roles: [
        {
          role: "ROLE",
          db: "DATABASE_NAME"
        }
      ]
    }
  )
successfully added user: {
  ...
}

## 参考

> [MongoDBコマンド集(ユーザ操作)](https://qiita.com/y-hara/items/83a86655bba48dc8b140)
> [MongoDBのユーザ管理](https://qiita.com/t2hk/items/45a04875dc6d8be9b004)
> [Error: couldn't add user: not authorized on test to execute command { createUser:](https://stackoverflow.com/questions/27784956/error-couldnt-add-user-not-authorized-on-test-to-execute-command-createuser)
> [mongodbを使ってみる (8) - ユーザー設定 -](https://kinjouj.github.io/2013/01/mongodb-8-user-configuration.html)
