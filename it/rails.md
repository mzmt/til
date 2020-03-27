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

- ポリモーフィック関連付けは両方を指定しないとindexが効かなそう
```ruby
e.g.
inner join users on users.attatchable_type = 'Post' and users.attatchable_id = posts.id
```

- updateする際、子レコードは親レコードが存在するかを確認するSQLを発行している(親が複数いる場合は全て)

## Rspec

- パフォーマンスの観点から、レコードを作らなくてすむ場合は作らないようにしたい。
モデルのユニットテストでも、作らなくてよいレコードを作っているケースはよくある。
```ruby
RSpec.describe User, type: :model do
  describe '#fullname' do
    let!(:user) { build :user, first_name: 'Shinichi', last_name: 'Maeshima' }
    it 'return full name' do
      expect(user.fullname).to eq 'Shinichi Maeshima'
    end
  end
end
```

User#fullnameはレコードが保存されているか否かに影響しないメソッドである。
この場合はcreateではなくbuild(もしくはbuild_stubbed)を使う。

https://github.com/willnet/rspec-style-guide#%E5%BF%85%E8%A6%81%E3%81%AA%E3%81%84%E3%83%AC%E3%82%B3%E3%83%BC%E3%83%89%E3%82%92%E4%BD%9C%E3%82%89%E3%81%AA%E3%81%84 


- リクエストスペックは、リクエストの文脈によって分けるのが良さそう

paramsとかでcotnextを切る

- is_expectedはexpect(subject)と一緒










