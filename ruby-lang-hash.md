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
h.to_a   #=> [["a", 100], ["b", 100], ["c", 300] ]
```

```ruby
```

```ruby
```