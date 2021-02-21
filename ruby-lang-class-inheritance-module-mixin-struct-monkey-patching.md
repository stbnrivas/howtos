# ruby objects, classes, structs , modules and mixins

`.`  is the access to module method operator
`::` is the access to module constant operator



ruby modules serve to include method into clases as instance method with `include` or class method with `extend`

```ruby
module Api
  module V1

    def get
      puts "get V1 version"
    end

    module Common
      def common
        puts "common works"
      end
    end
  end

  module V2
    include Api::V1::Common

    def get
      puts "get V1 version"
    end

  end
end



class Example
  include Api::V1::Common
  include Api::V2
end


e = Example.new
e.get
e.common


class StaticExample
  extend Api::V1::Common
  extend Api::V2
end

StaticExample.get
StaticExample.common

```


ruby support two sintax for nested modules


```ruby
# syntax 1
module API
  module V1
  end
end


# syntax 2
module API
end
module API::V1
end

# but there are NOT interchangeables
# - sintax 2 require that API module already exist
```


include using absolute path or relative path

```ruby
module Foo
  class Engine < Rails::Engine
  end
end

and

module Foo
  class Engine < ::Rails::Engine
  end
end

::Rails::Engine #is an absolute path to the constant.
# like /Rails/Engine in FS.

Rails::Engine #is a path relative to the current tree level.
# like ./Rails/Engine in FS.
```

```ruby

module ModuleX
  class CoolClass
  end
end

# equivalent

class ModuleX::CoolClass
end
```


## module, include vs extend

```ruby
module A
  def method_of_a
    puts "a"
  end
end

class ClassIncludeA
  include A
end

ClassIncludeA.new.method_of_a # a
ClassIncludeA.method_of_a # NoMethodError: undefined method method_of_a for ClassIncludeA:Class

class B
  extend A
end

ClassIncludeA.new.method_of_a # NoMethodError: undefined method method_of_a for ClassIncludeA:Class
ClassIncludeA.method_of_a # a
```

## including modules into modules, include or extend





## classes in ruby

Ruby has one simply rule: It's never allower access to anothers objects's instance variables. you need explicitly define setter and getter

```ruby
String.new.class.superclass.superclass
String.new.class.ancestors
String.new.methods

String.new.methods - String.new.class.superclass.methods
```


a simple inheritance example

```ruby
class Car
  def drive
      "from 0 to 100 at 10 seconds"
  end
end

class FastCar < Car
  def drive(top_speed)
      super() + "in turbo mode from 0 to #{top_speed} 10 seconds"
  end
end
```

don't need write setter and getters

```ruby
class Example
  attr_reader :name
  attr_accessor :age
private
  attr_writer :nickname
end
```


defining methods over instance,

```ruby
class Player
  def play_game
    rand(1..100)>50? "winner" : "loser"
  end
end

player = Player.new

def player.cheat
  "winner"
end

player.cheat
player.singleton_methods
player.singleton_class
```

instance variables using `@`


```ruby
class Duck
    attr_reader :name
    attr_accessor :surname
    attr_writer :nick

    @@class_variable = "quack!!"

    def initialize(name)
        @name = name
        @surname = nil
        @nick = nil
    end

    def property
        @property
    end

    def property=(new_property)
        @property = new_property
    end

    def to_s
        @@class_variable
    end
end
```


writing an inherited class

```ruby
class Parent
    def initialize
        @greeting = "greetings"
    end

    def salute
        @greeting
    end
end

class Son < Parent
    def initialize
        super
    end

    def informal
        "howdy"
    end
end
```

you can't overloading methods, you can put logic that branches depending on how many and what kinds of objects were passed



defining virtual attribute, its a calculated value or derived from one or more different instance


```ruby
class Arc
    attr_accessor :radians

    def degrees
        @radians * 180 / Math::PI
    end

    def degrees=(degrees)
        @radians = degrees * Math::PI /180
    end
end
```


delegating methods calls to another object

```ruby
require "delegate"
class OrdinalNumber < DelegateClass(Fixnum)
    def to_s
        delegate_s = __getobj__.to_s
        suffix = "st"
        return delegate_s + suffix
    end
end
```

delegating without access to specific methods


```ruby
class ArrayOnlyAppendable
    extend Forwardable
    def initialize
        @array = []
    end

    def_delegator :@array, :<<
end
```


```ruby
a = ArrayOnlyAppendable.new
a << 4 # right
a.size # undefined method 'size'
```

accepting or passing a variable number of arguments


```ruby
def sum(*numbers)
    numbers.inject(0){|sum,x| sum+=x}
end
```

duplicate or copy and object to modify

```ruby
instance_name.clone
instance_name.dup
```



## modules and namespaces

a module is a container of methods and constants,
a module create namespaces for methods with the same name
a module cannot be used to create instances
a module can be mixed into classes to add behaviour
a module can be used simulate multiple inheritance with mixins

are written in CamelCase name like class
constant should be written in UPPERCASE fully
access to methods module with dot  ModuleName.
access to constant with :: symbol (scope resolution operator)


using module for namespace container

```ruby
module Scoping
  class OriginalClassName
  end
end

# without include
c = Scoping::OriginalClassName.new

# with include
include Scoping
c2 = OriginalClassName.new
```





```ruby
module Taggable
    attr_accessor :tags

    COOL_CONSTANT = "cool"

    def taggable_setup
        @tags = []
    end

    def add_tag(tag)
        @tags << tag
    end

    def rem_tag(tag)
        @tags.delete(tag)
    end

    def self.default_tags
        ['untaggable','default']
    end
end

class TaggableString < String
    include Taggable
    def initialize(*args)
        super
        taggable_setup
        end
    end
end

Taggable::default_tags
ts = TaggableString.new
ts.add_tag("awesome")
ts.add_tag(Taggable::COOL_CONSTANT)
```

example of diferents namespace with modules

```ruby
module Square
    def self.area(side)
        side*side
    end
end
module Rectange
    def self.area(length,width)
        length*width
    end
end

class Shape
    include Square
    include Rectangle

    def using(side)
        Rectangle::area(side)
    end
end
```


Extending specific objects with modules, if you add module into class parents it will give a every string with tag I don't want this

```ruby
class Person
    def initialize(name)
        @name = name
    end
end

module SuperPowerOfFly
    def superpower
        "fly"
    end
end

clark_kent = Person.new("Clark Kent")
clark_kent.extend(SuperPowerOfFly)
clark_kent.superpower
```

classes are open ever


```ruby
class MyClass
  def initialize(value)
    @value = value
  end
end

my_instance = MyClass.new(20)
my_instance.instance_eval{ puts @value }

my_instance.instance_exec('executing into class',0) do |text, n|
  puts @value * n
end
```


defining a Class method using module

```ruby
module Runner
    def self.run
        "run forest run"
    end
end

class Man
    include Runner
    def run
        Runner.run
    end
end

Runner.run
m = Man.new
m.run
```


nesting modules

```ruby
module Player
  module InstanceMethods
    def play
        @status = "playing"
    end
    def stop
        @status = "stop"
    end
  end
  module ClassMethods
    def supported_formats
      ['flac','mp3']
    end
    def factory_static
        instance = new
        instance
    end
  end
end

class Audio
    include Player::InstanceMethods
    extend Player::ClassMethods
end


a = Audio.new
a.start

Audio.supported_formats


new_audio = Audio::factory_static
```





## Mixins

a mixin is a module that inject additional behaviour into a class
mixins allow us to simulate inheritance multiple
a class that include a module has access to its methods and constants
constant and methods mixed into a class do not need to be prefixed with the module name


while that inheritance is "is-a" relationship, mixins are "has-a" ModuleName feature set by example a String has a Comparable feature set

```ruby
class OlympicMedal
    # <,<=, >, >=, <=>, .between?
    include Comparable

    MEDAL_VALUES = {"Gold"=>3,"Silver"=>2,"Bronze"=>1}
    attr_reader :type

    def initialize(type, weight)
        @type = type
        @weight = weight
    end

    def <=>(other)
        -1 if MEDAL_VALUES[type] < MEDAL_VALUES[other.type]
        1 if MEDAL_VALUES[type] > MEDAL_VALUES[other.type]
        0 if MEDAL_VALUES[type] == MEDAL_VALUES[other.type]
    end
end
```




# Structs

```ruby
Struct.new(:name,:surname,:address)
```


# monkey patching

refers to the process of modifying or adding features to a predefined class to an existing class. What this means is even after whe have a class definition we can later reopen it and change things into this class

```ruby
puts [1,2,3].sum
class Array
    def sum
        total = 0
    end
end
puts [1,2,3].sum
```







# advanced tips

1. why to prefer accessing instance variables via attribute methods generated by `attr_reader :instance_var`



from [https://ivoanjo.me/blog/2017/09/20/why-i-always-use-attr_reader-to-access-instance-variables/](https://ivoanjo.me/blog/2017/09/20/why-i-always-use-attr_reader-to-access-instance-variables/)

```ruby
def engine
  @engine
end

# same but preferred below one

attr_reader :engine
```

For example

```ruby
class CarNotPreferred
  def initialize(owner)
    @owner = owner
    @engine = "wrrrooom"
  end

  def start(user)
    puts engine if user == @owner
  end

  private

    def engine
      @engine
    end
end
```



I used to prefer:

 - use attr_reader at the top of the class it serves as documentation
 - if the class don't have attr_writter or attr_accessors you can quickly know if the class is mutable/inmutable (the object itself this is not cover references)
 - easy and fast refactor, it becomes a lot easier to later refactor it, without needing to update all the places where it is used.

 - if you use attr_reader, you get better error description when instance variable is undefined
```ruby
# we create a new method `consume` with a typo error

class CarNotPreferred
  def initialize(owner)
    @owner = owner
    @engine = "wrrrooom"
  end

  def start(user)
    puts engine if user == @owner
  end

  def consume
    @my_engine.count("o").to_s + "l/km"
  end

  private

    def engine
      @engine
    end
end

c = CarNotPreferred.new("me")
c.consume

# NoMethodError (undefined method `count' for nil:NilClass)

```

 - if you use attr_writer


```ruby
class CarPreferred
  attr_reader :owner

  private

  attr_reader :engine

  public

  def initialize(owner)
    owner = owner
    engine = "wrrrooom"
  end

  def start(user)
    puts engine if user == owner
  end

  def consume
    my_engine.count("o").to_s + "l/km"
  end

end

c = CarPreferred.new("me")
c.consume

# undefined local variable or method `my_engine'
```


2. [ktop mentor of exercism] Here is the way that I organize my code:

I like to organize my code like this:

    class or module definition
    constants
    class methods
    private methods
        This includes initialize which is by default private.
            And initialize should be first
    protected methods
    public methods
    end class or module definition

The reason for the private and protected methods coming first is that by the time I get down to the public methods, I will have at least had a chance to see the names of the methods that are likely to be used in the public methods. No need to see something that I am not familiar with, scroll down to find out about the details, and scroll back up the file to the public methods.


3. [Ktop mentor of exercism]

Every time we use a local variable assignment, it might be that we can refactor that to a method. It provides the naming benefit, but also helps us to tell a better story.