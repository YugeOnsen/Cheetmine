## 目次
1. [入り方](#chapter1)
2. [ユーザの作成](#chapter2)
3. [データベースの作成・削除](#chapter3)
4. [テーブルの作成・削除](#chapter4)
5. [シーケンスの作成](#chapter5)
<br>

<a id ="chapter1"></a>

1. 入り方
   <br>
   <code>
   $ sudo -u postgres -i
   </code>
   <br>
   <code>
   $ sudo -U 名前 -h localhost -d データベース名
   </code>
   <br>

<a id ="chapter2"></a>

2. ユーザの作成
   <br>
   コマンド
   <br>
   <code>
   postgres@machine1:~$ createuser --createdb --username=postgres --pwprompt [ユーザー名]
   </code>
   <br>
   解説
   <br>
   --createdb : データベースの作成の許可
   <br>
    --username : PostgreSQLに接続するユーザー名 （postgresを指定しているのでスーパーユーザーで接続）
    <br>
    --pwprompt : パスワードを設定するためにプロンプトを表示
    <br>
<a id ="chapter3"></a>

3. データベースの作成・削除
    <br>
    - 作成
    <br>
    <code>
    $ postgres@machine1:~$ createdb sample_db --encoding=UTF-8 --lc-collate=C --lc-ctype=C --owner=anonymous --template=template0
    </code>
    <br>
    <br>
    コマンドの解説
    </b>
    <br>
    --encoding : DBの文字コードを指定する（UTF-8, EUC-JP, LATIN1 etc...）
    <br>
    --lc-collate : 文字列の並び順を指定する（C, ja_JP.UTF-8, en_US,UTF-8 etc...）
    <br>
    文字列ソートに影響
    --lc-ctype : 文字の種類を指定する
    <br>
    文字置換に影響（半角・全角）
    --owner : オーナーを指定する
    --template : ベースとなるDBを指定する
    <br>
    template0はまっさらなDBを作成し、template1の場合は複製される
    <br>
    <br>
    - 削除
    <br>
    <code>
    $ dropdb データベース名;
    </code>
    <br>
<a id ="chapter4"></a>

4. テーブルの作成・シーケンスの作成・削除
    <br>
   - テーブルの作成
   <br>
   <code>
   CREATE TABLE weather (
    <br>
    city            varchar(80),
    <br>
    temp_lo         int,           -- 最低気温
    <br>
    temp_hi         int,           -- 最高気温
    <br>
    prcp            real,          -- 降水量
    <br>
    date            date
    <br>
    ); 
    </code>
    <br>
    <br>
    PostgreSQLはint、smallint、real、double precision、char(N)、varchar(N)、date、time、timestampやintevalにサポート
    <br>
    <br>
    変数の型の後ろに[]をつけることで配列になる
    <br>
    例: int[]
    <br>
    <br>
    - テーブルの削除
    <br>
    <code>
    DROP TABLE テーブル名;
    </code> 
    <br>
<a id = "chapter5"></a>

5. シーケンスの作成
    <br>
    1から始める場合
    <br>
    <code>
    create sequence シーケンス名;
    </code>
    <br>
    101から始める場合
    <br>
    <code>
    create sequence シーケンス名 start 101;
    </code>
    <br>
    シーケンスで管理している連番の数字の「次の番号」を取得する際には「nextval」という関数を利用する。
    <br>
    <code>
    insert into abc (aID, bName, cDate)
values (nextval('シーケンス名'), 'おんせん', '2020-02-02');
    </code>
    <br>
    <br>
    最初からテーブルで作成(楽)
    <br>
    <code>
    create table abc (
    <br>
    aID serial PRIMARY KEY,
    <br>
    bName text NOT NULL,
    <br>
    cDate timestamp NOT NULL);
    </code>
    <br>
