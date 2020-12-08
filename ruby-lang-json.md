ruby json


```ruby
require 'json'
my_object = { :array => [1, 2, 3, { :sample => "hash"} ], :foo => "bar" }
puts JSON.pretty_generate(my_object)
```