## ReactアプリケーションにNode.jsとMySQLを使用したコンポーネントを作成する方法

### 前提条件
- ReactとNode.jsがインストールされていること。
- MySQLサーバーがセットアップされていること。

### ステップ

1. **Node.jsのセットアップ**
   - Express.jsを使用してサーバーサイドの基盤を作成します。

2. **MySQLデータベースへの接続**
   - `mysql` パッケージを使用してMySQLデータベースに接続します。

3. **APIエンドポイントの作成**
   - Reactアプリケーションから呼び出すためのREST APIエンドポイントを作成します。

4. **Reactコンポーネントの作成**
   - データベースからデータを取得し、表示するためのReactコンポーネントを作成します。

### 実装例

1. **Expressサーバーの設定**

   ```javascript
   const express = require('express');
   const mysql = require('mysql');
   const app = express();
   const port = 3001;

   // MySQL接続設定
   const connection = mysql.createConnection({
     host: 'localhost',
     user: 'root',
     password: 'password',
     database: 'mydb'
   });

   // データベース接続
   connection.connect();

   app.get('/api/data', (req, res) => {
     // MySQLクエリを実行
     connection.query('SELECT * FROM mytable', (err, results, fields) => {
       if (err) throw err;
       res.json(results);
     });
   });

   app.listen(port, () => {
     console.log(`Server running on port ${port}`);
   });
