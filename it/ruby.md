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

`<`   はクラス継承しているかのチェックにも使える
```ruby
if 1.class < Numeric  # true
```

public_send

publicなメンバにしかアクセスできないsendメソッド

https://docs.ruby-lang.org/ja/latest/method/Object/i/public_send.html

===

```ruby
if (1..10) === 5 then         # Range
  puts "OK"
end

if /[a-z]/ === "a" then       # Regexp
  puts "OK"
end

if String === "a" then        # Module
  puts "OK"
end
```
 
SecureRandom.alphanumeric(5)
文字列だけでランダムな値を生成できる

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

# inheritance
- メソッドを呼び出す順番

`hoge.ancestors`で呼び出す。継承リストの上から呼び出す。見つからない場合は、`method_missing`を探し出す
`ancestors`は`class`, `superclass`と違いmoduleを表示する

- `Module#prepend`

`include`と同じくmoduleをmixinするメソッド。includeと違い、mixinされた先のクラス内のメソッドより先に呼ばれる。
ancestorsで見るとmixin先より継承リストの上にあることがわかる。

- 特異クラス(singleton_class)

各オブジェクトが必ず1つ持っているクラス。

- 特異メソッド

インスタンスに対して定義されているメソッド。そのインスタンスのクラスよりも継承リストの上位にあるので、先に呼ばれる。

- `extend`

include, prependと同じくmixinのメソッドだが、特異クラスにmixinする。
```ruby
module Mod
    def homu
        "Mod#homu"
    end
end

class X
end

x = X.new

# Mod のメソッドが x オブジェクトに定義される
x.extend Mod

p x.homu
# => "Mod#homu"

```



