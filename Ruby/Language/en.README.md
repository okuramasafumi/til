# Ruby Language

## `send`, `method_missing` and private method

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

This code generates the output like this:

```
method_missing
1
```

`warn` method call is caught by `method_missing`, but `send(:warn, 1)` call is not and instead calls `Kernel#warn`.

It turned out that `send` can call private methods and methods in `Kernel` module are all private.

## Method definition

* When we define more than one method with the same name, the later-defined one will be used.
