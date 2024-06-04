# Larabel の学習

## 前提

- WSL の ubuntu 24 を使う
- php を入れる
- composer を入れる
- mariadb を入れる。DBを作り、ユーザーを作り、権限を与えておく。あとで、`.env`に書き込まなければならないので覚えておく。

```shell
sudo apt install php
sudo apt install composer
sudo apt install mariadb-server

# mariadb (sqlサーバー)にログイン
sudo mysql -u root
```

```sql
-- hoge はユーザー名, fuga はパスワード
create user 'hoge'@'localhost' identified by 'fuga';

-- laravel というデータベースを作る。後述の .env では、データベースのデフォルト名は laravel になっている。なんでもよい。
create database laravel;

-- 上記データベース内の全テーブルに対する全権限を、上記のユーザーに与える。
grant all on laravel.* to hoge@localhost
```

### 要求された php モジュール

`php --ini` や `php -m` で確認。<br />
`apt search` や `apt show` で調べる。

- mbstring
- mysql
- xml

---

## やったこと

### Larabel 10 プロジェクト作成

```shell
composer create-project laravel/laravel laravel_study "10.*"

# 私の場合、上記の操作中に、php-xml が無いことでエラーが出た。インストールしてやりなおした。

# 作成後は package.json をもとに node_modules を作成
cd laravel_study
npm i
```

### app.php 編集

```php
// タイムゾーン
'timezone' => 'Asia/Tokyo',

// 言語
'locale' => 'ja',

// 偽データ生成ツールを使う時の言語
'faker_locale' => 'ja_JP',
```

### Breeze インストール

[参照](https://laravel.com/docs/11.x/starter-kits#laravel-breeze-installation)

対話型インストールにおいては、当面の練習のため、とりあえず Blade を使う方向で選択。
慣れたら、他の選択肢を検討。

```shell
# インストーラのようなものをインストール
composer require laravel/breeze --dev

# インストール開始
php artisan breeze:install

# インストール後の処置
php artisan migrate
npm i
```

####  Breeze 日本語化

次を参照

[https://github.com/askdkc/breezejp](https://github.com/askdkc/breezejp)

