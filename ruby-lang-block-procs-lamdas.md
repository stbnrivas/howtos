# block
- a block is not an object
- a block is a collection of code to be executed
- blocks must be attached to a method call
- blocks alter the execution of the method
- a block is not an argument / parameter to the method

```ruby
[2,5,7,9].each {|n|puts n**2 }
# 
[2,5,7,9].each do |n|
  puts n**2
end
```


# yield
 
yield transfer control from the method to the block that is attached to the method call


```ruby
def pass_control
    puts "before"
    yield
    puts "after"
end

pass_control { puts "inside the block" }
pass_control # error invalid block
```


```ruby
def who_am_i
    user = yield
    puts "I am #{user}"
end

who_am_i { "groot" }
```


```ruby
def multiples_pass
    yield
    yield
end

multiples_pass { "inside" }
```

```ruby
def pass_control_on_condition
    yield if block_given?
end
pass_control_on_condition
pass_control_on_condition{"inside"}
```

yielding with arguments

```ruby
def yielding_with_argument
    yield "argument"
end
yielding_with_argument {|s| puts s}
```


```ruby
def yielding_with_argument(argument)
    yield argument
end
yielding_with_argument("hello world") {|s| puts s}
```


# procs

a procs is an objects that essentially as a saved block

```ruby
a = [1,2,3]
b = [4,5,6]
c = [0,0,0]

a.map {|n| n**2}
b.map {|n| n**2}
c.map {|n| n**2}

#
square = Proc.new {|n| n**2}

a.map(&square)
b.map(&square)
c.map(&square)
```

```ruby
currencies = [10,20,30,40]
to_euros = Proc.new{ |currency| currency*0.95}
to_pesos = Proc.new{ |currency| currency*20.67}

currencies.map(&to_euros)
currencies.map(&to_pesos)
```

```ruby
age = [10,18,22]
is_older = Proc.new do |age|
    age > 18
end
ages.select(&is_older)
age.reject(&is_older)
```

invoking a proc

```ruby
example = Proc.new { puts "hi there" }
example.call
```


# custom each

```ruby
def custom_each(array)
    i = 0
    while i < array.length
        yield array[i]
        i+=1
    end
end

names = ["John","Jane"]
numbers = [1,2,3,4]

custom_each(names) do |name|
    puts name.length
end

custom_each(numbers) do |number|
    puts n
end
```


```ruby
["1","2","3"].map(&:to_i)
[1,2,3].select(&:even?)
```

pass a proc as argument

```ruby
def passing_a_proc_as_argument(name,&myproc)
    myprc.call
end

pr1 = Proc.new do |name|
    puts name
end

passing_a_proc_as_argument("hello world",&pr1)
```


## lambdas in ruby

lambdas are objects but procs are not objects. you can use a lambda anywhere can use a proc

```ruby 
squares_proc = Proc.new { |number| number**2}
[1,2,3].map(&squares_proc)
squares_proc.call(5)

squares_lambda = lambda {|number| number **2}
[1,2,3].map(&squares_lambda)
squares_lambda.call(5)
```

lambdas and procs seems the same but ... they treat the wrong number of arguments

```ruby
some_proc = Proc.new do |name,age|
    puts "#{name} #{age}"
end
some_proc.call("john doe",42)
some_proc.call

some_lambda = lambda { |name,age| puts "#{name} #{age}" }
some_lambda.call("john doe",42)
some_lambda.call() # => wrong number of arguments ...
```