# Dockerのコンテナ、イメージを削除する

## Dockerのコンテナを削除する: `docker rm`

```
$ docker rm CONTAINER_ID
```

`CONTAINER_ID`: コンテナID

## Dockerのイメージを削除する: `docker rmi`

```
$ docker rmi IMAGE
```

`IMAGE`: イメージ(リポジトリ名 / イメージID)

## Docker一括削除

### すべて

停止コンテナ、タグ無しイメージ、未使用ボリューム、未使用ネットワークの一括削除

```bash
$ docker system prune
```

### コンテナ

#### 停止コンテナ

```bash
$ docker container prune
```

#### 全コンテナ

```bash
$ docker rm -f (docker ps -a -q)
```

### イメージ

#### 未使用イメージ 

```bash
$ docker image prune
```

#### タグ無しイメージ

```bash
$ docker rmi (docker images -f "dangling+true" -q)
```

### ボリューム

```bash
$ docker volume prune
```

### 未使用ネットワーク

```bash
$ docker network prune
```
