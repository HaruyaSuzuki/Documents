# Docker

## 流れ
イメージを作成し、それを元にコンテナを作成する。

## コマンド一覧
- docker images: 現在あるイメージの一覧を出力。
- docker run [イメージ名]: イメージを起動。
- docker-compose up -d --build: コンテナを起動。
- docker-compose exec python3 bash: bashでコンテナへ接続。
- docker exec -it python3 [コマンド]: コンテナ内で作業。
- docker ps: 現在起動して居るコンテナが分かる。
- docker ps -a: 終了したコンテナ含めて表示。
- docker stop [コンテナid]: コンテナの実行を終了。
- docker rm [コンテナid]: コンテナを削除。
- docker rmi [イメージ名]: イメージを削除。
- docker down: コンテナごと削除。
- exit: コンテナから脱出。