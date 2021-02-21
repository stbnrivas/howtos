# the tap method

 yield self to the block and then return self

```ruby
user = User.new.tap do |u|
  u.build_profile
  u.process_credit_card
  u.ship_out_item
  u.send_email_confirmation
  u.blahblahblah
end
```


# interesting function of String

- convert an String to array to use enumerable

```ruby
"asdfg".split ""
```

```ruby
"asdfg".chars
```




# interesting functions of enumerable

- each

- first, last

- take, drop

- any?

- all?

- none?

- one?





- flatten
```ruby
[[1,2],3,[[4]]].flatten
#=> [1, 2, 3, 4]
```


- map
```ruby
(1..9).map {|x| x+1}
# => [2, 3, 4, 5, 6, 7, 8, 9, 10]
```

- flat_map
```ruby
(1..9).flat_map {|x| [x+1]}
```



- collect (works like `map` but it is more semantic than map)
```ruby
(1..9).collect { "wtf" }
```


- collect_concat (it works like `flat_map` but is more semantic than map)
```ruby
{ one: {id: 1, "name_one"}, two: {id: 2, "name_two"} }
(1..9).collect_concat { 10 }
```









- filter
```ruby
(1..9).filter {|x| x.even? }
# => [2, 4, 6, 8]
```

- filter_map
```ruby
(1..9).filter_map { |i| i * 2 if i.even? } #=> [4, 8, 12, 16, 20]
```




- find
```ruby
(1..9).find { |i| i.even? } #=> 2
```

- find_all
```ruby
(1..9).find_all { |i| i.even? } #=> [4, 8, 12, 16, 20]
```


- select, select!
```ruby
[1,2,3,4,5,6].select { |n| n.even? }
# => [2, 4, 6]

[1,2,3,4,5,6].select(&:even?)
# => [2, 4, 6]

('a'..'z').select.with_index { |value, index| index.even? }
# => ["a", "c", "e", "g", "i", "k", "m", "o", "q", "s", "u", "w", "y"]
```

- reject, reject!
```ruby
[1,2,3,4,5,6].reject { |n| n.odd? }
# => [2, 4, 6]

[1,2,3,4,5,6].reject(&:odd?)
# => [2, 4, 6]

('a'..'z').reject.with_index { |value, index| index.odd? }
# => ["a", "c", "e", "g", "i", "k", "m", "o", "q", "s", "u", "w", "y"]
```








- inject
```ruby
[1, 2, 3, 4, 5].inject do |memo, value|
   memo += value
end
# => 15

[1, 2, 3, 4, 5].inject(:+)
# => 15



a = [['A', 'a'], ['B', 'b'], ['C', 'c']]
a.inject({}) do |m,v|
	m[v[0]] = v[1]
	m
end
# => {"A"=>"a", "B"=>"b", "C"=>"c"}
```

- reduce
```ruby
[1, 2, 3, 4, 5].reduce do |memo, value|
   memo += value
end
# => 15


[1, 2, 3, 4, 5].reduce(5, :+)
# => 15

```


- detect


















- zip
- unzip


- sort
```ruby

```













- take_while
```ruby

```

- group_by
```ruby
x =  (0..9)
x.group_by{ |i| i%3 }
# {0=>[0, 3, 6, 9], 1=>[1, 4, 7], 2=>[2, 5, 8]}
```

- each_slice
```ruby
x = (1..9)
x.each_slice(3){ |slice| p slice}

#[1, 2, 3]
#[4, 5, 6]
#[7, 8, 9]

x.each_slice(3){ |slice| p slice.first}

#[1, 4, 7]
```


- partition
```ruby
x = (1..9)
x.partition(&:odd?)

# [[1, 3, 5, 7, 9], [2, 4, 6, 8]]
```