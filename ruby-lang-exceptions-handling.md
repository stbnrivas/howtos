# handling exceptions in ruby

from [https://es.slideshare.net/ihower/exception-handling-designing-robust-software-in-ruby](https://es.slideshare.net/ihower/exception-handling-designing-robust-software-in-ruby)

thanks @wen-tien Chang


```
if code in one routine encounters an unexpected condition that it does not know how handle, it throws an exception, essentially throwing up its hands and yelling. "I do not know what tod do about this, i suer hope somebody else knos how to handle it"
Steve McConnel, Code Complete
```

```
raising an exception means stopping normal excution of the program an either dealing with the problem that's been encountered or exiting the program completely
David A. Black, The well-grounded rubyist
```

```
In practice, the rescue clause should be a short sequence of simple instructions designed to bring the object back to a stable state and to either retry teh operation or terminate with failure
Bertrand Meyer, Object Oriented Software Construction
```


```
ask yourself, Will this code still run if I remove all the execptions handlers? if the answer is no, then maybe exceptions are being used in non-exceptional circumstances
Dave Thomas and Andy Hunt, The pragmatic programmer
```

```
Exceptions should be used for exceptional behaviour. They should not acts as substitute for conditional test. If you can reasonably expect the caller to check the condition before calling the operation, you should provide a test, and the caller should use it
```


```
In most cases, the caller should determine how to handle an error, not the callee
Brian Kernigham and Rob Pike, The Practice of Programming
```


## raise exception

```ruby
begin
	raise 'Shit happens'
rescue => e
	puts "I am rescued"
	puts e.message
	puts e.backtrace.inspect
end


begin
	fail 'Shit happens'
rescue => e
	puts "I am rescued"
	puts e.message
	puts e.backtrace.inspect
end
```

```
I almost always use the "fail" keyword. The only time I use "raise" is weh i am catching and exception and re-raising i, because here I'm not failing, but explicitly an purposefully raising an exception
Jim Weirich, Rake author
```

# raise signature

```ruby
raise(exception_class_or_object, message, backtrace)

raise # equivalent raise RuntimeError
raise RuntimeError # equivalent raise

raise "shit happens"
raise RuntimeError, "shit happens"

raise RuntimeError, "shit happens"
raise RuntimeError.new("shit happens")

raise RuntimeError, "shit happens"
raise RuntimeError, "shit happens", caller(0)
```


## global $! variable

```ruby
$!
$ERROR_INFO
# reset to nil if the expeption is rescued
```


## rescue

```ruby
# a simple exception rescue
rescue SomeError => e
end

# multiple exception rescue in single block
rescue SomeError, SomeOtherError => e
end

# multiple exception rescue in differents block
rescue SomeError => e
rescue SomeOtherError => e
end
```

## ruby exception hierarchy

```
Exception
├── NomemoryError
│   
├── ScriptError
│   ├── LoadError
│   ├── NotImplementedError
│   └── SyntaxError
│   
├── SecurityError
│   └── LoadError
│   
├── SignalException
│   └── Interrupt
│   
├── StandardError --default for rescue
│   ├── ArgumentError
│   │   └── UncaughtThrowError
│   │
│   ├── EncodingError
│   │
│   ├── FiberError
│   │
│   ├── IOError
│   │   └── EOFError
│   │
│   ├── IndexError
│   │   ├── KeyError
│   │   └── StopIteration
│   │
│   ├── LocalJumpError
│   │
│   ├── NameError
│   │   └── NoMethodError
│   │
│   ├── RangeError
│   │   └── FloatDomainError
│   │
│   ├── RegexpError
│   │
│   ├── RuntimeError -- default for raise
│   │
│   ├── SystemCallError
│   │   └── Errno::*
│   │
│   ├── ThreadError
│   │
│   ├── TypeError
│   │
│   └── ZeroDivisionError
│   
├── SystemExit
│   
├── SystemStackError
│   
├── SyntaxError
└── StandardError
```



## ActiveSupport can suppress

```ruby
# ActiveSupport has
# http://api.rubyonrails.org/classes/Kernel.html#method-i-suppress
suppress(Exception) do
   # dangerous code here
end

suppress(IOError, SystemCallError) do
	open("NONEXISTENT_FILE")
end
puts 'this code gets executed'

# without ActiveSupport we can do
def suppress(*exception_classes)
	yield
rescue
end
```



```ruby
# selecting by message error
def errors_with_message(pattern)
	m = Module.new
	m.singleton_class.instance_eval do
		define_method(:===) do |e|
			pattern === e.message
		end
	end
	m
end
begin
  raise "Timeout ends while reading in socket"
rescue errors_with_message(/socket/)
  puts "ignoring timeout"
end


# 
def errors_matching(&block)
	m = Module.new
	m.singleton_class.instance_eval do
		define_method(:===, &block)
	end
	m
end


begin 
	raise "timeout..."
rescue errors_matching{|e| e.message =~ /timeout/}
	puts "ignoring timeout"
end
```





## ensure

```ruby
begin 
	raise "error ..."
rescue => e
	puts "rescued"
ensure
	puts "this code is always executed"
end
```


## retry

```ruby
tries = 0
begin 
	tries +=1
	puts "trying #{tries}"
	raise "It didn't work"
rescue
	retry if tries < 3
	puts "I give up"
end
```


## else

```ruby
begin 
	yield
rescue
	puts "only if error"
else 
	puts "only if success"
ensure
	puts "always executed"
end
```



## wrapping exception

```ruby
class MyError < StandardError
	attr_reader :original
	def initialize(msg, original=$!)
		super(msg)
		@original = original
		set_backtrace original.backtrace
	end
end

# or better
module MyLibrary
	class Error < StandardError
	end
end
```

## using timeout with exceptions

```ruby
begin 
	Timeout::timeout(3) do
	end
rescue Timeout::Error => e
	# 
end
```



## operational errors vs programmer errors

example operational errors:

- failed to connect to server
- failed to resolve hostname
- request timeout
- server returned a 500 response
- socket hang-up
- system is out of memory

we can handle operational errors, restore and cleanup resource, handle it directly, propagate, retry, crash, log it

example programmer erro "like typo"

we should not handle programmer errors



## robust

- robustness: teh ability of a system to resist change without adapting its initial stable configuration

### four level of robustness [wikpedia link](https://en.wikipedia.org/wiki/Robustness)

- level 0

	+ service: failing implicitly or explicitly
	+ state: unknown or incorrect
	+ lifetime: terminated or continued

- level 1 Error-reporting (failing fast)

	+ service failing explicitly
	+ state: unknown or incorrect
	+ lifetime: terminate or continued
	+ how-achieved: propagating all unhandled exceptions and catching and reporting them in the main programs

- level 2 state-recovery (weakly tolerant)

	+ service: failing explicitly
	+ state: correct
	+ lifetime: continued
	+ how-achieved: backguard recovery, cleanup

- level 3 behavior-recovery (strongly tolerant)

	+ service delivered
	+ state correct
	+ lifetime continued
	+ how-achieved: retry, and/or. design diversity, data diversity and functional diversity


Which adopt: 
- level 0 is insufficient, beeter reach level 1
- level 2 for critical operation, storage, database...
- level 3 for critical feature or customer requires, it means cost*2 two solutions


## failure reporting 

- log system, central log server
- email
- 3rd party log system(airbrake, sentry new relic)