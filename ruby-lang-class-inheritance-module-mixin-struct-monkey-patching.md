#ruby objects and classes

Ruby has one simply rule: It's never allower access to anothers objects's instance variables. you need explicitly define setter and getter

```ruby
String.new.class.superclass.superclass
String.new.class.ancestors
String.new.methods

String.new.methods - String.new.class.superclass.methods
```



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



# modules and namespaces

a module is a container of methods and constants,
a module create namespaces for methods with the same name
a module cannot be used to create instances
a module can be mixed into classes to add behaviour
a module can be used simulate multiple inheritance with mixins

are written in CamelCase name like class
constant should be written in UPPERCASE fully
access to methods module with dot  ModuleName.
access to constant with :: symbol (scope resolution operator)


```ruby
module Taggable
    attr_accessor :tags

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



# Mixins

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