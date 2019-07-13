## 概要
Apache2.4 + PHP7.3 + MySQL8.0 の環境を構築します。

## 使い方
1. プロジェクトをクローンします。
```
git clone https://github.com/katsuobushiFPGA/docker-lamp.git
```
2. web/project以下にプロジェクトソースを入れます。
3. docker-compose.yml の DocumentRootをプロジェクトのDocumentRootに合わせます。(※デフォルトは `/var/www/html` です。)  
```
args: 
  DOCUMENT_ROOT: /var/www/html
```
例: project以下の `public` フォルダをドキュメントルートにする場合、下記のように設定する必要があります。
```
args: 
  DOCUMENT_ROOT: /var/www/html/public
```
4. MySQLの初期データの投入
`db/init/1_create_db.sql` に使用するデータベース名を記載します。
`db/init` 以下に `.gz` 形式のファイルもしくは `.sql`ファイルを格納します。
5. Dockerのビルド + 起動
```
docker-compose up -d
```
6. http://localhost もしくは https://localhost でアクセスできます。