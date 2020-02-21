# Rails

## ActiveRecord

- 評価タイミング

ActiveRecord::FinderMethodsに実装されているメソッド
```
find, find_by, take, first, last, exists?
```
はすぐにクエリを発行する。

それ以外の検索メソッド(where, limit, など)
はActiveRecord::Relationのオブジェクトを返し、実際にデータが必要になるタイミングまでデータベースにはアクセスしない。遅延評価(Lazy Evaluation)

https://qiita.com/ykamez/items/0c81a33ec1b90219d541
