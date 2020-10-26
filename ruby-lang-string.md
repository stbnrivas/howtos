# String.new

new(str="", capacity: size) → new_str
s = String.new("", capacity: 200) → new_str

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
a.size
a.length
```


```ruby
s = "aabbcc"
s.delete("a") # => "bbcc"
s2 = "hello world with vocals"
s2.delete("aeiou") # => "hll wrld wth vcls"
```

```ruby
s = "aabbccdd"
s.each_byte{|c| print c, " "} # 97 97 98 98 99 99 100 100
s.each_char{|c| print c, " "} # a a b b c c d d 

"hello\nworld".each_line {|s| p s}
# "hello\n"
# "world"
a = "abcde"
a.chars.map{|x| x.upcase}
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
"   hello   ".strip # => "hello"
"   hello world   ".strip # => "hello world"

"   hello   ".lstrip # => "hello   "
"   hello   ".rstrip # => "   hello"

"hello".ljust(5)    # => "hello"
"hello".ljust(6)    # => "hello "
"hello".ljust(10)    # => "hello     "

"hello".rjust(5)  #=> "hello     "
"hello".rjust(6," ")  #=> " hello"
"hello".rjust(10)  # => "     hello"
```


```ruby
"Ruby".match?(/R.../) # => true

```


```ruby
s = "part1;part2"
s.split("part1;part2")
# => ["part1","part2"]
```


```ruby
s = "this is a string"
s.slice!(0)        #=> "t"
s.slice!(1)        #=> "h"
s.slice!(2)        #=> "i"
s.slice!(3..6)     #=> " is "
s = "this is a string"

s = "part1;part2"
s.tr("a","o") # => "port1;port2"
s.tr("","") # => "this is a string"
s = "replacing all vocals for"
s.tr("aeiou","_") # => "r_pl_c_ng _ll v_c_ls f_r"
rna = "CATAATG"
rna.tr("AG","_X") # => "C_T__TX"
s.tr!
```



```ruby
# string
"[%10s]" % "carrot"    # paddging: "[    carrot]"
"[%-10s]" % "carrot"   # negative padding "[carrot    ]"

# decimal
"Number is %d" % 12

# float-pointing
"Result is %.2f" % 12.3456
"Result can be %.2f %.2f %.2f" % [12.3456,12.43545,765.4656456]


"name %{b} age %{z}" % {b: "John", z: 58}

Kernel::sprintf("There are %d units.", 10)
```