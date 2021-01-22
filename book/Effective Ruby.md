Rubyのメソッド走査
階層構造を下から辿っていく

moduleをincludeする時、superclassメソッドなどからは見えないが、includeしたクラスの上にクラスとして挿入される。
この時、moduleは１つ上のクラスになるので、includeしたクラスのメソッドをオーバーライドすることはできない。

特異クラス
継承階層に含まれる、他からは見えないクラス。
```ruby
customer = Customer.new

def customer.name
  'aaaaa'
end
```

この場合、nameメソッドはcustomer専用になる。
ほとんどのクラスは、そのクラスから生成されるオブジェクトのためにメソッドを格納しているが、
特異クラスは１つのオブジェクトのために働く。
```ruby
class Base
  def nyan(args)
  end
end

class User < Base
  def nyan(args)
    # nyanをオーバーライドしている。スーパークラスのnyanをどうやって呼ぶか
  end
end
```

この場合は`super(args)`を使う
