# Ruby Language

## `send`, `method_missing`とプライベートメソッド

```ruby
class Foo
  def method_missing(meth, *args, &blk)
    puts "Warn: #{args}" if meth == :warn
  end
end

bar = Foo.new
bar.warn(1)
bar.send(:warn, 1)
```

このコードの出力は以下のようになる。

```
method_missing
1
```

`warn`は`method_missing`に補足されるが、`send`のほうは補足されずに`Kernel#warn`が呼び出されている。

これは`send`がプライベートメソッドを呼べ、かつ`Kernel`モジュールのメソッドは全てプライベートメソッドであることが理由だった。

## メソッド定義

* 同名のメソッドは後から定義されたものが優先される
