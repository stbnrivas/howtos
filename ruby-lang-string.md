# String.new

new(str="", capacity: size) → new_str

The optional capacity keyword argument specifies the size of the internal buffer. This may improve performance, when the string will be concatenated many times (causing many realloc calls).

```ruby
a = "Hello "
a << "World"
a << 33 # => "Hello World!"

a = "0123456789"
a[2,3] # => "234"
a[2..3] # => "23"
```

```ruby
a = "Hello World"
a.capitalize
a.capitalize!
a.downcase
a.downcase!
a.upcase
a.upcase!
"abcd".succ        #=> "abce"
```

```ruby
a.empty?
a.count
a.size
a.length
```


```ruby
s = "aabbcc"
s.delete("a") # => "bbcc"
```

```ruby
s = "aabbccdd"
s.each_byte{|c| print c, " "} # 97 97 98 98 99 99 100 100
s.each_char{|c| print c, " "} # a a b b c c d d 

"hello\nworld".each_line {|s| p s}
# "hello\n"
# "world"
```


```ruby
"hello".eql?("hello")

"hello".end_with?("ello")     #=> true
"hello".end_with?("heaven", "ello")     #=> true
"hello".end_with?("heaven", "paradise") #=> false

"hello world".include?("llo")   #=> true
```


```ruby
# gsub - return a copy of str with all occurrences
# gsub!

"hello".gsub(/[aeiou]/, '*')    # => "h*ll*"
```



```ruby
"hello".ljust(4)    # => "hello    "
"    hello    ".lstrip()    # => "hello    "
s = "    hello    "
s.lstrip!()    # => "hello    "

"  hello  ".rstrip   #=> "  hello"
"  hello  ".rstrip!  #=> "  hello"

"hello".rjust(4)
"hello".rjust(20)  #=> "               hello"
"hello".rjust(20," ")  #=> "               hello"
```


```ruby
"Ruby".match?(/R.../) # => true

```


```ruby
s = "this is a string"
s.slice!(2)        #=> "i"
s.slice!(3..6)     #=> " is "
s = "this is a string"

s.split(' ')

s = "thes es o streng"
s.tr("e","i") # => "this is o string"
s.tr("eo","ia") # => "this is a string"
s.tr!
```


```ruby
a = "abcde"
a.chars.map{|x|puts x}
```