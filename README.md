<p align="center">
    <a href="https://laravel.com"><img alt="Laravel v10.x" src="https://img.shields.io/badge/Laravel-v10.x-FF2D20?style=for-the-badge&logo=laravel"></a>
    <a href="https://php.net"><img alt="PHP 83" src="https://img.shields.io/badge/PHP-8.3-777BB4?style=for-the-badge&logo=php"></a>
</a>
</p>

## セットアップ

### データベース名やホスト名などの一括置換

- DB名は `appdb`で検索して置換する。
- Dockerのコンテナ名やネットワーク名は `__tmp__`で検索して置換する。

### 初回実行

```bash
sudo chmod 777 -R ./
# Windowsの場合、cnfファイルの権限が「777」だと読み込みされずに無視されてしまう
sudo chmod 644 ./docker/mysql/my.cnf
```

```bash
# ホスト側で実行
docker compose up -d --build
docker compose exec app bash

# コンテナ内で実行
npm install
composer install
cp .env.example .env
php artisan key:generate
php artisan storage:link
php artisan migrate:fresh --seed

# 権限エラーになったら実行
chmod 644 -R storage/logs/
chmod 644 -R storage/framework/

```

### 2回目以降

```bash
# コンテナの起動
docker compose start

# コンテナの停止
docker compose stop
```

### 環境が壊れたら

```bash
# 消滅の呪文
docker compose down --rmi all --volumes --remove-orphans

# 復活の呪文
docker compose up -d --build
```