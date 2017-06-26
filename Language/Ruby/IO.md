# Ruby IO

* [IO in Ruby](https://robots.thoughtbot.com/io-in-ruby)
* [Quick tips for doing IO with Ruby](https://mauricio.github.io/2014/08/03/quick-tips-for-doing-io-with-ruby.html)

## Closing Stream

Close the stream to flush Ruby's buffer and release the file descriptor back to the OS.

```ruby
# Use File.open with block to flush and close automatically
File.open('some-file.txt', 'w') do |f|
  f.write('test')
end
```

## StringIO

It makes a `String` look like an `IO` object, hence the name `StringIO`. `StringIO` has `read` and `write` methods, so it can be passed to parts of your code that were designed to read/write from files or sockets. However, it is not exactly like a `File`.

