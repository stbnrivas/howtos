# Hash.new {}

```ruby
options = { font_size: 10, font_family: "Arial" }
options[:background_color] = 'black'

options.delete(:background_color)
options.delete_if {|key, value| key >= "b" }
```




```ruby
h = { "a" => 100, "b" => 200, "c" => 300 }
h.select {|k,v| k > "a"}  #=> {"b" => 200, "c" => 300}
h.select! {|k,v| k > "a"}  #=> {"b" => 200, "c" => 300}
```

```ruby
h = { "a" => 100, "b" => 200, "c" => 300 }
new_sintax = { key: 'value' }
h.to_a   #=> [["a", 100], ["b", 100], ["c", 300] ]
```

```ruby
h = { "a" => 100, "b" => 200 }
h.fetch("a")                            #=> 100
h.fetch("z", "go fish")                 #=> "go fish"
h.fetch("z") { |el| "go fish, #{el}"}   #=> "go fish, z"
```

```ruby
a = {1=> "one", 2 => "two", 3 => "three", "ii" => "two"}
a.rassoc("two")    #=> [2, "two"]
a.rassoc("four")   #=> nil
```


```ruby
h = { a: 100, b: 200, c: 300 }
h.slice(:a)           #=> {:a=>100}
h.slice(:b, :c, :d)   #=> {:b=>200, :c=>300}
```