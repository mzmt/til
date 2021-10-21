# Rails

## tips
validationの行を項目ごとに分けると、エラーが出た時にどのエラーか分かりやすい

`validates :num, presence: true, numericality: { greater_than: 0 }`
みたいに書くと、開発時のエラー画面で`presence`と`numericality`のどっちに引っかかってるか分からないが、

```ruby
validates :num, presence: true,
                numericality: { greater_than: 0 }
```
のように書くと該当箇所がハイライトされる

## method

`try`
オブジェクトがnilでない場合のみ、そのオブジェクトのメソッドを実行する

```ruby
user ? user.age : "年齢なし" #userがいるか確認している
user.try(:age) || "年齢なし" #userがいるか確認していない
```

```
名前: <%= @user.name unless @user.nil? %>
```

```
名前: <%= @user.try(:name) %>
```
これを
```
User.try(:find, 1)
```
こう書ける。引数も渡せる

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

- increment, or decrimentメソッド

特定のレコードの値を増やしたり減らしたりできる. !をつけるとsaveはいらなくなる
```ruby
User.first.increment!(:point, 2000)
```

pick  
```ruby
User.where("age > 20").limit(1).pluck(:id)).first
User.where("age > 20").pick(:id)

// 実装
def pick(*column_names)
  limit(1).pluck(*column_names).first
end
```
https://github.com/rails/rails/pull/31941

saveでレコードが保存できないとき
```ruby
post.save  // failed
post.errors.full_messages  // check error
```

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

JSを使わないと実行できない操作は以下のようにする
```
it 'hoge', js: true do
~ ~ ~
end
```
https://qiita.com/jnchito/items/607f956263c38a5fec24#javascript%E3%82%92%E4%BD%BF%E3%82%8F%E3%81%AA%E3%81%84%E3%81%A8%E6%93%8D%E4%BD%9C%E3%81%A7%E3%81%8D%E3%81%AA%E3%81%84%E5%87%A6%E7%90%86%E3%82%92%E3%83%86%E3%82%B9%E3%83%88%E3%81%99%E3%82%8B

User#fullnameはレコードが保存されているか否かに影響しないメソッドである。
この場合はcreateではなくbuild(もしくはbuild_stubbed)を使う。

https://github.com/willnet/rspec-style-guide#%E5%BF%85%E8%A6%81%E3%81%AA%E3%81%84%E3%83%AC%E3%82%B3%E3%83%BC%E3%83%89%E3%82%92%E4%BD%9C%E3%82%89%E3%81%AA%E3%81%84 


- リクエストスペックは、リクエストの文脈によって分けるのが良さそう

paramsとかでcotnextを切る

- is_expectedはexpect(subject)と一緒


capybaraで、デバッグ時にレンダリングされるhtmlを整形して表示する方法
```
puts CGI.pretty(page.body)
```

## other gems
count(*)しなければページネーションできないので、レコード数が多いとkaminariが遅くなる問題
`without_count`オプションで解決する
https://thr3a.hatenablog.com/entry/20180313/1520902569
