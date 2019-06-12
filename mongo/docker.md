# MongoDBをDocker上で動かす場合



## Docker Compose

```yaml
version: "3.1"

services:
  mongo:
    image: mongo
    restart: always
    volumes:
      - ./mongo/data:/data/db
      - ./mongo/init:/docker-entrypoint-initdb.d
    ports: 
      - 27017:27017
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGODB_ROOT_USERNAME}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGODB_ROOT_PASSWORD}
      MONGO_INITDB_DATABASE: ${MONGO_INITDB_DATABASE}

  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - 8081:8081
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: ${MONGODB_ROOT_USERNAME}
      ME_CONFIG_MONGODB_ADMINPASSWORD: ${MONGODB_ROOT_PASSWORD}
```

### 環境変数

- `MONGO_INITDB_ROOT_USERNAME`: MongoDBの管理者権限(admin)を持つユーザの名前
- `MONGO_INITDB_ROOT_PASSWORD`: MongoDBの管理者権限(admin)を持つユーザのパスワード
- `MONGO_INITDB_DATABASE`: インスタンスを作ったときに最初に作るデータベースの名前

### 初期実行スクリプト

任意のパス(今回は`./mongo/init`)を`/docker-entrypoint-initdb.d`にマウントすることで`./mongo/init`に格納されている`*.js`ファイルを実行する。
以下のjsファイルはデータベース`DATABASE_NAME`に対して読み書きできるユーザを追加するスクリプトである。

```javascript
var users = [
  {
    user: 'USERNAME',
    pwd: 'PASSWORD',
    roles: [
      {
        role: "readWrite",
        db: 'DATABASE_NAME',
      }
    ]
  }
];

for (var i = 0, length = users.length; i < length; ++i) {
  db.createUser(users[i]);
}
```
