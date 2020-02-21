# Ruby

## method
update_all
- アクティブレコードのObjectを経由しないので早い

concat
- 破壊的に連結する

e.g.
```ruby
[1,2,3].push([1,2])
=> [1, 2, 3, [1, 2]]

[1,2,3].concat([1,2])
=> [1, 2, 3, 1, 2]
```
# Rails


# general
- クエリ件数が多い時は、１件ずつupdateせずに、UPDATE文を100件ずつまとめて発行数を削減する
