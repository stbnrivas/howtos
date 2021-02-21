# Array.new

```ruby
a = Array.new    #=> []
a = Array.new(3)       #=> [nil, nil, nil]
a = Array.new(3, true) #=> [true, true, true]
a = Array.new(2, Hash.new) # => [{}, {}] 2 elements are same hash reference
a = Array.new(2) { Hash.new } # [{},{}]
a = Array.new(4) {|i| i.to_s } #=> ["0", "1", "2", "3"]
a = Array.new
a[4] = "4";                 #=> [nil, nil, nil, nil, "4"]
```

```ruby
a = [0,1,2,3,4,5]
a[0] # => 0
a[100] # => nil
a[-1] # => 5
a[-2] # => 4
a[-6] # => 0
a[-7] # => nil
a.at(0) # => 0
a.at(-1) # => 5
a.fecth(100)  #=> IndexError: index 100 outside of array bounds: -6...6
arr.fetch(100, "oops") #=> "oops"
```


```ruby
a = [0,1,2,3,4,5]
a.take(0) # => []
a.take(3) # => [0,1,2]
a.take(45) # => [0,1,2,3,4,5]

a.drop(0) # => [0,1,2,3,4,5]
a.drop(1) # => [1,2,3,4,5]
a.drop(45) # => []
```

```ruby
[ "a", nil, "b", nil, "c", nil ].compact #=> [ "a", "b", "c" ]
```


```ruby
[ *'a'..'z' ]  # => ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"]
```



```ruby
a = [0,1,2]
a.length # => 3
a.count # => 3
a.count { |x| x%2 == 0 } # 2
a.size # => 3
a.empty? # => false
```


```ruby
a = [0,1,2]
a.include?(2) # => true
a.include? 4 # => false
```


```ruby
a = [] 
a.push(0) # [0]
a.push(1) # [0,1]
a << 2 # [0,1,2]
a.insert(0,-1) # [-1,0,1,2]
a.insert(0,-3,-2) # => [-3, -2, -1, 0, 1, 2]
a.unshift(-4) # => [-4, -3, -2, -1, -1, 0, 1, 2]
a.shift # => -4 
puts s # => [-3, -2, -1, -1, 0, 1, 2]

a = [ 1, 2 ]
a << "c" << "d" << [ 3, 4 ] # #=>  [ 1, 2, "c", "d", [ 3, 4 ] ]
```


```ruby
a = [0,1,2,3]
a.push 4 # => [0,1,2,3,4]
a.pop # => 4
a # [0,1,2,3]
a.shift # => 0
a # [1,2,3]
a.delete_at(0) # => 1
a # [2,3]
a.delete_at(-1) # => 3
a # [2]
array_with_nil = [0,nil,1,nil,2,nil]
array_with_nil.compact # => [0, 1, 2]
array_with_nil.compact! # => [0, 1, 2]
```



```ruby
a = [0,1,2,3,4,5,6,7]
a.each {|e| print e, " "}

a = [ "a", "b", "c" ]
a.each_index {|x| print x, " " } # 0 1 2 3
 
a.reverse_each {|e| print e, " "}
a.map {|e| 2*e}
a.map! {|e| 2*e}
```


```ruby
a = [0,1,2,3,4,5,6,7]
a.select{|e| e%2==0} # => [0,2,4,6]
a.select!{|e| e%2==0} # => [0,2,4,6]

a.reject{|e| e%2==0} # => [1,3,5,7]
a.reject!{|e| e%2==0} # => [1,3,5,7]
```




´´´ruby
[ 1, 2, 3 ] + [ 4, 5 ]    #=> [ 1, 2, 3, 4, 5 ]
´´´



```ruby
# bsearch {|x| block } → elem
a = [0, 4, 7, 10, 12]
a.bsearch {|x| x >= 4 } #=> 4

# bsearch_index {|x| block } → int or nil
a = [0, 4, 7, 10, 12]
a.bsearch_index {|x| x >= 4 } #=> 1

a = [ "a", "b", "b", "b", "c" ]
a.index("b")             #=> 1
a.rindex("b")            #=> 3
```


```ruby
[].eql?[] # => true

```


```ruby
a = [[1, 2], 3, [4, 5, 6, [7, 8]], 9, 10]
a.flatten # => a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
a.flatten!

[ "a", "b", "c" ].join        #=> "abc"
[ "a", [1, 2, [:x, :y]], "b" ].join("-")   #=> "a-1-2-x-y-b"

a.min
a.max
```



```ruby
a = [1,2,3,4,5,6]
a.keep_if{|item| item%2==0} # => [2, 4, 6]
```


```ruby
a=[1,2,3]
a.permutation.to_a  #=> [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
a.permutation(1).to_a  #=> [[1],[2],[3]]
```


```ruby
a = [ "a", "b", "c", "d" ]
a.rotate         #=> ["b", "c", "d", "a"]
```


```bash
[1,2,3,4,5].select { |num|  num.even?  }   #=> [2, 4]
```