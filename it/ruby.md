# Ruby

## method
update_all
- アクティブレコードのObjectを経由しないので早い

AとBが比較できるかを知りたい時は
```ruby
(A <=> B).nil?
```

concat
- 破壊的に連結する

e.g.
```ruby
[1,2,3].push([1,2])
=> [1, 2, 3, [1, 2]]

[1,2,3].concat([1,2])
=> [1, 2, 3, 1, 2]
```

block_given?
- メソッドにブロックが渡されているかどうかを返す
```ruby
def method
  yield if block_given?
end

method(args) { another_method }
```

delegate

https://docs.ruby-lang.org/ja/latest/method/Forwardable/i/delegate.html

メソッドの委譲先を指定できる。これもわかりやすい

https://magazine.rubyist.net/articles/0012/0012-BundledLibraries.html


# general
- クエリ件数が多い時は、１件ずつupdateせずに、UPDATE文を100件ずつまとめて発行数を削減する

リフレクション
> プログラムの(実行前ではなく)実行時にプログラムそのものの情報を参照・書き換えることができる特性

よく分かんない。パーフェクトRubyの10章読むといいらしい

https://www.xmisao.com/2013/12/13/ruby-reflection-method-summary.html
wikipedia
https://en.wikipedia.org/wiki/Reflection_%28computer_programming%29

# exception
- rescueで型を指定しない場合は、StandardErrorをrescueする
- StandardErrorをrescueした場合、StandardErrorとそのサブクラスがrescueされる



