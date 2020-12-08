# metaprogramming in ruby


```ruby
define_method(:new_method) do |arg = nil|
	puts "into"
end
new_method


define_method(:other_method) do |*args|
	puts "into with #{args[0]}"
end
other_method "value"
```



```ruby
eval('(2+3).times {|n| puts n}')
```


```ruby
a = Array.new
def a.is_fully_empty?
  true
end

a.is_fully_empty?
```

