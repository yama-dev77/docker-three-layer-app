# 🐳 Docker 削除コマンド 完全チートシート

Docker の削除系コマンド（コンテナ / イメージ / ネットワーク / ボリューム / system）を  
ひとつにまとめた完全版チートシートです。

## 1. コンテナ削除（Container）
### 特定コンテナ削除
```
docker rm <container>
```
### 実行中コンテナ強制削除
```
docker rm -f <container>
```
### 停止中すべて削除
```
docker container prune
```
### 全コンテナ削除（危険）
```
docker rm -f $(docker ps -aq)
```

## 2. イメージ削除（Image）
```
docker rmi <image>
docker image prune
docker image prune -a
docker rmi $(docker images -q)
```

## 3. ボリューム削除（Volume）
```
docker volume rm <volume>
docker volume prune
docker volume rm $(docker volume ls -q)
```

## 4. ネットワーク削除（Network）
```
docker network rm <network>
docker network prune
```
※ 以下は削除不可: bridge / host / none

## 5. system prune
```
docker system prune
docker system prune -a --volumes
```

## 6. docker compose
```
docker compose down
docker compose down -v
docker compose down --remove-orphans
```

## 7. 補助コマンド
```
docker ps -a
docker images
docker volume ls
docker network ls
```
