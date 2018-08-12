# Metaprogramming

* [Please stop calling it "magic"](https://zverok.github.io/blog/2017-10-22-stop-magic.html)

## instance_eval

If you want to add methods to an instance "on-the-fly". Notice that it affect this particular "instance" only and not the whole class. All the other instances of the same class will not be affected.

```ruby
s = 'hello.world'
s.instance_eval do
  def /(delimiter)
    split(delimiter)
  end
end

# Can also be used to access private methods
class User
  private
  
  def secret_key
    '???'
  end
end

u = User.find(1)
u.instance_eval('@secret_key')
```

## class_eval and module_eval

Adding methods/attributes to a class/module "on-the-fly". This will affect all instances later.

`class_eval` is an alias to `module_eval`

```ruby
# Just like opening the class and do extension
String.class_eval do
  def how_many
    size
  end
end
```

