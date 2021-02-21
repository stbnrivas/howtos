# scala classes

  + a scala source file can contain multiple clasess
  + fields in classes come with getter and setters
  + car replace a field getter/setter with a custom one
  + can use @BeanProporty annotation to getXxx / setXxx
  + every class has a primary constructor


```scala
class Counter {
	private var value: Int = 0
	def increment(): Unit = { value += 1}
	def current(): Int = value
}

val counterOne = new Counter
val counterTwo = new Counter()

counterOne.current
counterOne.current()

counterOne.increment
counterOne.increment()

```

- properties with getter and setters


```scala
class Person {
	var age = 0
}

val p: Person = new Person
p.age
p.age = 23
// mutated p.age

p.age_=(21)


// redefining getter and setters
class Person {
	private var privateAge: Integer = 0

	def age(): Int = privateAge
	def age_=(newAge: Int):Unit = {
		if(newAge > privateAge) privateAge = newAge
	}
}

val p: Person = new Person
p.age
p.age = 23
p.age_=(21)
p.age
```

  + if the field is private getter and setter are private
  + if the field is a val, only getter is generated
  + if the field is a var, setter and getter is generated
  + if you don't want getter or setter declare as `private[this]`



- bean properties

```scala
class Person {
	@scala.beans.BeanProperty  var name: String = _
}

val p: Person = new Person

p.name
p.name="john doe"
p.getName()
p.setName("jane doe")
```


- primary constructor

```scala
class Person(val name: String, var age: Int){
	// the params of primary constructor turns into field that are
}

val p = new Person("john",34)
p.name
p.age

// name, are val no mutated
p.name = "jane" // fail
p.age = 35 // success
```

```scala
class Person(val name: String, var age: Int){
	var status: String = if (age > 90) "tired" else "well"
	// initialization are all statements in the class definitions.
}
val p = new Person("john",34)
```


```scala
class Person {
	// if there are not param after the class, the class has
	// primary constructor without parameters
}
```


```scala
class Person private(val id: Int){
}
```

- auxiliary constructors

  + the auxiliary constructor are called this
  + each  auxiliary constructor must start with a call to a previously defined auxiliary constructor or the primary constructor

```scala
class Person {
	private var name: String = ""
	private var age: Integer = 0

	def this(name: String) = {
		this() // like super
		this.name = name
	}

	def this(name: String, age: Int) = {
		this(name)
		this.age = age
	}
}

// note that don't indicate what return
```

- calling superclass constructor (only)

```scala
class FourLeggedAnimal {
	println("into FourLeggedAnimal primary constructor")
    def walk { println("I'm walking") }
    def run { println("I'm running") }
}

class Dog extends FourLeggedAnimal {
	println("into Dog primary constructor")
    def walkThenRun {
        super.walk
        super.run
    }
}
val dog = new Dog
dog.walkThenRun
```


- nested classes

```scala
import scala.collection.mutable.ArrayBuffer

class Network {
	class Node(val mac: String){
		val contacts = new ArrayBuffer[Node]
	}

	private val members = new ArrayBuffer[Node]

	def join(mac: String): Node = {
		val m = new Node(mac)
		members += m
		m
	}
}
```



- scala anonymous classes

```scala
class CustomLog(val prefix: String) {
	def shortLogMessage(message: String): Unit = {
		val timestamp : Long = DateTime.now(DateTimeZone.UTC)
		println(s"$timestamp: $message")
	}
}

val anAnonymousClassInstance = new CustomLog {
	override def shortLogMessage(message: String): Unit = { println(s"$message")}
}


/*
class CustomLog_Anonymoys_12324324342 extends CustomLog {
	override def shortLogMessage(message: String): Unit = { println(s"$message")}
}
val anAnonymousClassInstance = new CustomLog_Anonymoys_12324324342
*/
```




# scala objects


use `Object` when you need a class with a single instance, or when you want to find a home for miscellaneous values or functions.


- for singletons and utility methods
- a class can have an object companion object with the same name
- Object can extedn classes or traits
- the apply method of an object is ussually used for constructing new instances of the companion class
- to avoid the main method, use an object that extends the App trait
- you can implement enumerations by extending the Enumeration object


## singleton

scala has not static method or fields, Instead use this

```scala
object Helper {
	private var text: String = ""
	def concatenator(s: String) = { text += s }
	def result(): String = { text }
}

Helper.result
Helper.concatenator("help")
Helper.result

```
## companion objects

in Java or C++, you often have a class with both instance methods and static method. In Scala you can achive this
by having a class and a "companion" object of the same name


```scala
class Person(val id :Int,val name: String) {

}

object Person {
	var get_id = scala.util.Random.nextInt
}

// ensure that use :paste in REPL
val p: Person = new Person(Person.get_id, "John")
p

Person.get_id
```


## objects extending a class or a trait


```scala
abstract class DoAble(val description: String) {
	def undo(): Unit
	def redo(): Unit
}

object DoNothingAction extends DoAble("empty") {
	override def undo(): Unit = {}
	override def redo(): Unit = {}
}
```


## the `apply` method


the apply method lives in any class in any object

```scala

object MySingleton {
	def apply(x: Int): Int = x +1
}

MySingleton.apply(1) // equivalent
MySingleton(1)       // equivalent

```



# inheritance

- use `extends` to indicate inheritance
- final classes can not be subclassed
- you must use override when override a method
- only the primary constructor can call the primary superclass constructor
- you can override fields


```scala
class Animal {}
class Dog extends Animal {}


class Person(name: String) {}
class Employee(name: String) extends Person(name) {
	var salary = 0.0
}
```

- overriding methods



```scala
class Car() {
	def maxSpeed(): Integer = { 100 }
}

class RedCar() extends Car {
	override def maxSpeed(): Integer = { 200 }
}
```


## type checks and casts


```scala
class Car() {}
class RedCar() extends Car {}

val c: Car = new Car
val r1: Car = new RedCar
val r2: RedCar = new RedCar

if (c.isInstanceOf[Car]) true else false
// true
if (c.isInstanceOf[RedCar]) true else false
// false

if (r1.isInstanceOf[Car]) true else false
// true
if (r1.isInstanceOf[RedCar]) true else false
// true

if (r2.isInstanceOf[Car]) true else false
// true
if (r2.isInstanceOf[RedCar]) true else false
// true


// cast

c.asInstanceOf[Car]

c.asInstanceOf[RedCar]  // java.lang.ClassCastException: Car cannot be cast to RedCar

r1.asInstanceOf[Car]
r1.asInstanceOf[RedCar]


c match {
	case c: RedCar => println("a Redcar")
	case c: Car => println("a Redcar")
	case _ => println("a Redcar")
}

// a Redcar

val i: Integer = 5
i match {
	case i: RedCar => println("a Redcar")
	case i: Car => println("a Redcar")
	case i: _ => println("a Redcar")
}
```


## overriding in a subclass

use override with val, var, and def to rewrite behaviour

```scala
class Person(val name: String){
	override def toString =s"${getClass.getName}[name=$name]"
}

val p: Person = new Person("john doe")

class SecretAgent(codeNumber: String) extends Person(codeNumber) {
	override val name = "secret"
	override val toString = "secret"
}
```


## abstrack classes

as in Java, you can use `abstract` to force a class can not be instantiated

```scala
abstract class PrePerson(val name: String){
	val birthday: Long // abstract field without initial value
	def id: Int // abstract method without implementation body
}

val p = new PrePerson("j") // error: class PrePerson is abstract; cannot be instantiated
```

concrete classes should provide abtract 

```scala
class Person(val name: String) extends PrePerson {
	val birthday: Long = java.lang.System.currentTimeMillis
	val name = name
}
```


## final classses


when you want prevent that any can override into subclass can use `final`

```scala
class Octopus(val arms: Integer){
	final val weight: Integer = 1
}

class MutantOctupus() extends Octopus(10){ }

// but
class MutantOctupus() extends Octopus(10){ 
	val weight: Integer = 10 // value weight cannot override final member
}


```

## lazy val declaration

```scala
// WRONG

class Octopus(val arms: Integer){
	val weight: Integer = 1
}

class MutantOctupus() extends Octopus(10){ 
	lazy val weight: Integer = 10 // value weight cannot override final member
}
```


## scala inheritance hierarchy

Any is a superclass

AnyVal and AnyRef extends Any

Unit extend AnyVal

TODO:


## Object Equality

`eq` method of the Anyref clas check whether two references refers to the same object

`equals` method is to overriding to provide a natural equality, if two items has same fields

```scala
final override def equals(other: Any) = {
	other.isInstanceOf[Item] && {
		val that == other.asInstanceOf[Item]
		description == that.description && price == that.price
	}
}

// using pattern matching

final override def equals(other: Any) = other match {
	case that: Item => description == that.description && price == that.price
	case _ => false
}
```



## Value Classes

some classes have a single field such as the wrapper classes for primitive types, `rich` or `ops` inefficiten, try define are inlined




# traits 

- In Java interfaces are restrictive, only have abtract methods and don't allow state it force to use abstract class and interfaces at the same time, but in scala trait can have state, val, var and implemented method.

- a class can extends one or more traits. A trait may require implementing classes to support ceratin features. Unlike Java
interfaces Scala traits can supply state and behavior for these features which makes them far more useful

- When you extends multiples traits, the order matters. Traits are constructed left-to-right.

- In scala when extends multiples traits arise conflict. pay attention about how scala solves conflict from multiple traits

- you can import Java interfaces, with sintax of extend

```scala
trait Logger {
	def log(msg: String) // An abstract method
}

class ConsoleLogger extends Logger {
	def log(msg: String) { println(msg) }
	// don't need to put override keyword
}
```


- extends multiples trait

```scala
class ConsoleLogger extends Logger with Serializable with AnotherTrait {
	def log(msg: String) { println(msg) }
	// don't need to put override keyword
}
```

- traits with concrete implementation

```scala
trait ConsoleLogger {
	def log(msg: String): Unit = { println(msg) }
}

class Operator extends ConsoleLogger {
	def basicOperation(): Unit = { log("Operator#basicOperationS")}
}

val o: Operator = new Operator
o.basicOperation

o.log // ERROR
```

- nesting trait 

```scala
trait Logger { def log(msg: String) }
trait ConsoleLogger extends Logger { def log(msg: String) { println(msg) } }
trait RemoteLogger extends Logger { def log(msg: String) { println(msg) } }

abstract class Operator extends Logger { def basicOperation(): Unit = { log("Operator#basicOperationS")} }

val opConsole: Operator = new Operator with ConsoleLogger
val opRemote: Operator = new Operator with RemoteLogger
```

- trait construction order (back to front)

TODO

```scala
NOT WORKING
trait APrefix { def prefix(msg: String): String = { s"A$msg"} }
trait BPrefix { def prefix(msg: String): String = { s"B$msg"} }

class CustomStringAB(s: String) extends APrefix with BPrefix {
	def text(msg: String): String = { prefix(msg) }
} 

val withA: CustomStringAB = new CustomStringAB("example") //with APrefix with BPrefix
```

- trait rich interfaces


```scala
trait Logger {
	def log(msg: String)
	def info(msg: String):   Unit = {log(s"INFO: $msg")}
	def warn(msg: String):   Unit = {log(s"WARN: $msg")}
	def severe(msg: String): Unit = {log(s"SEVERE: $msg")}
}

abstract class Operation extends Logger {
	def basic(): Unit = { info("example") }
}
```

- concrete fields in traits

```scala
trait WithState {
	val simple = 15
}

class Example extends WithState {}

val e: Example = new Example
e.simple
```

- abstract fields in traits


```scala
trait WithStateAbstract {
	val simple: Int
}

abstract class ExampleAbstract extends WithStateAbstract {}

class ExampleConcrete extends WithStateAbstract {
	val simple: Int = 15
}
```


- initializing trait fields (solving construction order)


```scala
trait FileLogger {
	val filename: String
	val out = new PrintStream(filename)
	def log(msg: String): Unit = { out.printl(msg)}
}

// with object
val logger = new { val filename = "myapp.log" } with Operation with FileLogger

// with class
class DifficultOperation extends { val filenam = "myapp.log" } with Account with FileLogger {

}

// using lazy
trait FileLogger extends Logger {
	val filename: String
	lazy val out = new PrintStream(filename)
	def log(msg: String) { out.println(msg) }
}

```


- trait extending classes

```scala
class Example {
	val x: Integer = 25
}

trait TraitExample extends Example {

}
// obviusly trait can not be instantiated
```
