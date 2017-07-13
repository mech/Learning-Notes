# Ruby IO

* [IO in Ruby](https://robots.thoughtbot.com/io-in-ruby)
* [Quick tips for doing IO with Ruby](https://mauricio.github.io/2014/08/03/quick-tips-for-doing-io-with-ruby.html)

## Closing Stream

Close the stream to flush Ruby's buffer and release the file descriptor back to the OS.

```ruby
# open is synonymous to new
File.open(path, 'w')
File.new(path, 'w')

# Use File.open with block to flush and close automatically
File.open('some-file.txt', 'w') do |f|
  f.write('test')
end
```

* r - Read-only mode. Default mode.
* r+ - Read-write mode. The file pointer will be at the beginning of the file.
* w - Write-only mode. Overwrites file if exists. If not, creates a new file.
* w+ - Read-write mode. Overwrites existing file. If not, creates a new file for reading and writing.
* a - Write-only mode. File pointer at the end of the file if file exists. If not, creates a new file for writing.
* a+ - Read-write mode.

## Existence of File

```ruby
File.exists?(path)

# A file may exist but have zero length
File.zero?(path)
```

## StringIO

It makes a `String` look like an `IO` object, hence the name `StringIO`. `StringIO` has `read` and `write` methods, so it can be passed to parts of your code that were designed to read/write from files or sockets. However, it is not exactly like a `File`.

## INODE