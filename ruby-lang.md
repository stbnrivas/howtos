# ruby

```ruby
MEAN_OF_LIFE = "42"
```



```ruby
puts "hello world"
puts "hello 
world"
print "hello"," world"
p "hello world"
```

```ruby
name = gets 
name = gets.chomp 
```


- parallel assignament

```ruby
a, b, c = 10, 20, 30
a, b = b, a
```


```ruby
x ||=y
# equivalent
unless x
    x = y
end
```



```ruby
x = y || z
# equivalent to
if y
    x = y
else 
    x = z

```


in ruby 'and' '&&' are differents, 'or' and '||' but both use short-circuit evaluation operator binaries has lower precedence, don't mixed in the same condition

The Ruby Style Guide says: Use &&/|| for boolean expressions, and/or for control flow. (Rule of thumb: If you have to use outer parentheses, you are using the wrong operators.)

* 'and' 'or' 'not' are control flow operator
* '&&' '||' '!' are binary operators

use control flow to things like

```ruby
p = Post.find_by_name('awesome post') and p.publish!
```