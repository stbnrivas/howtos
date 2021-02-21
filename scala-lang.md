# about scala

- Scala combines object-oriented and functional programming in one concise, high-level language.

- Scala's static types help avoid bugs in complex applications

- Scala has insteresting features as:
 + currying
 + type inference
 + immutability
 + lazy evaluation
 + pattern matching

- In Scala we usually operatte with INMUTABLE values/object. Ergo, any MODIFICATION to an object must return ANOTHER object. as benefits:
 + an easily multithreading/distributed environment adoption
 + helps making sense of the code "reasing about the code"
 + it makes scala a better aproach to object oriented "alan key oop interpretation"

# installation scala language installation



requirements:

 - sdkman


```bash
sudo apt-get install zip unzip
curl -s "https://get.sdkman.io" | bash

sdk version
sdk list java

sdk install java
sdk install ant

```


```bash
sdk upgrade scala
sdk uninstall ant 1.9.9
```


```bash
scala -version
```



# compilation and running

```scala
// HelloWorld.scala
object HelloWorld {
	def main(args: Array[String]){
		println("Hello world")
	}
}
// a object is a singleton
```



```bash
scalac HelloWorld.scala
scalac HelloWorld.scala -deprecation

ls
# 'HelloWorld$.class'   HelloWorld.class   HelloWorld.scala
scala HelloWorld
```

# scala repl

```
scala

	:quit
	quit

sbt console
```






# language concepts: val (value) var (variable)

- comments

```scala
// single line comments

/*
 multi line comments
*/
```

- datatypes

all in scala is an object (there are not primitive)

```scala
val i: Integer = 1
val l: Long = 1L
val d: Double = 4.0
val f: Float = 4.0f
val b: Boolean = true
val c: Char = 'c'

val t:(Integer,String,Double) = (0,"one",2.0)
val s:String = t._2

// Unit
// AnyVal
// AnyRef
// ANY
// Null an AnyRef without value
// Option
// Nothing all types at same time
```




- literals, is data that apperas directly in the source like number 5. scala has integer literals, character literals, string literals and function literals

- val

```scala
val x: Int = 5
res0: Int = 5

(x: Int) => x + 2
res1: Int => Int = $$Lambda$763/645208036@426e505c

```

- interpolation into string

```scala
val str = "hello"
println(s"$str world")
```

- a value is an inmmutable, typed storage unit. A value can be assigned data when it is defined but can never be reassigned


```scala
val <name>: <type> = <literal>
val x: Int = 5
```

- type interface

```scala
val x = 20
val greetings = "Hello World"
```

- variables

```scala
var x = 20
var greetings = "Hello World"
```

- Unit

Unit in scala is like void, null, nil


- functions or method

```scala
def functionExample(a: String): String =  a

def functionExample(a: String): Unit =  a


def functionExample(a: String): Unit =  a
```

- anonymous functions

```scala
(x:Int) => x +1 
// res4: Int => Int = $$Lambda$843/2075339084@f391e52

(z:Int, y:Int)=> z*y
```


# string in scala

```scala
val msg1 = "john" + "doe" + 1
val msg2 = s"$msg1 rules"
val t = ("john","doe")
val msg3 = s"${t._2}, ${t._1}"
```


# statements and expressions


# lambda expressions (anonimous functions)

```scala
val square = x => x*x
def square(x:Double):Double = x*x

val twice: Doble => Double = _ *2
```

functions are first class citizen

```
val add2 = adder(2, _:Int)
add2: (Int) => Int = <function1>
```


partial application

curried functions

```
def multiply(m: Int)(n: Int)(o: Int): Int = m * n * o
multiply(2)(3)(4)
multiply(1) _
```


# class in scala

```
class Calculator(model_: String) {
  // Constructors aren’t special methods, they are the code outside of method definitions in your class
  val brand: String = "HP"
  val color: String = "Black"
  val model: String = model_
  def add(m: Int, n: Int): Int = m + n
}

val calc = new Calculator("Casio")
calc.color
```


scala doesn't support static classes or class method, but scala has singleton that don't have instances. 


```scala
object TestClass {
	def sum(a: Int, b: Int): Int = a + b
	def del(a: Int, b: Int): Int = a - b
}
```


```scala
object Application {
	def main(args: Array[String]): Unit = { println("Hello world")}
}
```


## inheritance

```
class ScientificCalculator(brand: String) extends Calculator(brand) {
  def log(m: Int): Double = log(m, math.exp(1))
}
```

abstract classes

```
abstract class Shape {
 def getArea():Int    // subclass should define this
}

class Circle(r: Int) extends Shape {
 def getArea():Int = { r * r * 3 }
}
```

## traits

```
trait Car {
  val brand: String
}

trait Shiny {
  val shineRefraction: Int

  def shine(): Unit = {
  	println("i cant see")
  }
}

class CoolCar extends Car with Shiny {
  val brand = "BMW"
  val shineRefraction = 12
}

// When do you want a Trait instead of an Abstract Class?
// favour the use the traits over Abstract Class because a class can extend only one class
// If you need a constructor parameter, use an abstract class. Abstract class constructors can take parameters; trait constructors can’t.
```

## apply methods


```scala
//apply methods give you a nice syntactic sugar for when a class or object has one main use.
class Some {}

object Factory {
  def apply() = new Some
}

val newSome = Factory()
```

the apply method has built because scala runs on the JVM but it is OO platform, how can OO platform build functional programming features as:

- compose functions
- pass functions as args
- return functions as result

functionX and apply method to the rescue:

functionX = Function1, Function2, Function3, Function4, ... Function22

 - Function1 a function with 1 arguments and 1 return value
 - Function2 a function with 2 arguments and 1 return value
 - Function3 a function with 3 arguments and 1 return value
 - Function4 a function with 4 arguments and 1 return value
 - ...
 - Function22 a function with 22 arguments and 1 return value

```scala
val simpleIncrementer = new Function1[Int,Int]{
	override def apply(arg: Int): Int = arg + 1
}
simpleIncrementer(1)
res3: Int = 2


val simpleIncrementer2 = new Function2[Int,Int,Int]{
	override def apply(arg1: Int, arg2: Int): Int = arg1 + arg2 + 1
}
simpleIncrementer2(1,5)


// sintactic sugar #1
val incrementer: Function1[Int,Int] = (x:Int) => x+1

// sintactic sugar #2
val incrementer: Int => Int = (x:Int) => x+1



Seq(1,2,3)
```









## objects

```scala
// Objects are used to hold single instances of a class. Often used for factories.
object Timer {
  var count = 0

  def currentCount(): Long = {
    count += 1
    count
  }
}

// Classes and Objects can have the same name. The object is called a ‘Companion Object’. We commonly use Companion Objects for Factories.
Timer.currentCount()
```


# pattern matching

```scala
val times = 1

times match {
  case 1 => "one"
  case 2 => "two"
  case _ => "some other number"
}

// with guards
times match {
  case i if i == 1 => "one"
  case i if i == 2 => "two"
  case _ => "some other number"
}

// patching on type
def bigger(o: Any): Any = {
  o match {
    case i: Int if i < 0 => i - 1
    case i: Int => i + 1
    case d: Double if d < 0.0 => d - 0.1
    case d: Double => d + 0.1
    case text: String => text + "s"
  }
}
```





# object

An object is a class that has exactly one instance. It is created lazily when it is referenced, like a lazy val.

```scala
object Box
```

Here’s an example of an object with a method:


```scala
package logging

object Logger {
  def info(message: String): Unit = println(s"INFO: $message")
}




import logging.Logger.info

class Project(name: String, daysToComplete: Int)

class Test {
  val project1 = new Project("TPS Reports", 1)
  val project2 = new Project("Website redesign", 5)
  info("Created projects")  // Prints "INFO: Created projects"
}
```


# companion object

A companion object in Scala is an object that’s declared in the same file as a class, and has the same name as the class

```
class Calculator {
	def printFilename() = {
        println(SomeClass.HiddenFilename)
    }
}

object Calculator {
	object SomeClass {
	    private val HiddenFilename = "/tmp/foo.bar"
	}
}
```
This has several benefits. First, a companion object and its class can access each other’s private members (fields and methods).
This means that the printFilename method in this class will work because it can access the HiddenFilename field in its companion object:



# case classes

Case classes are like regular classes with a few key differences which we will go over. case classes are lightweight data structures with some boilerplate

- sensible equals, copy and hash code
- companion with apply
- serialization (useful for akka)
- companion with apply
- pattern matching


1. You can construct them without using new.

```scala
case class Book(isbn: String)

val frankenstein = Book("978-0486282114")
```

2. You can’t reassign, case classes reassign this is discouraged.


```scala
case class Book(isbn: String)

var frankenstein = Book("978-0486282114")
frankenstein.isbn = "WRONG!!!!!"
```

3. Instances of case classes are compared by structure and not by reference:

```scala
case class Message(payload: String)

val message2 = Message("01010101001111")
val message3 = Message("01010101001111")

val messagesAreTheSame = message2 == message3  // true
```

4. You can create a (shallow) copy of an instance of a case class simply by using the copy method

```scala
case class Message(payload: String, sender: String, recipient: String)

val message1 = Message("01010101001111","#2345","#6436")
val message2 = message1.copy(sender = "#2345", recipient= "#6437")
```

5. differences between

Case classes are good for modeling immutable data. case classes are used to conveniently store and match on the contents of a class.


```scala
case class Calculator(brand: String, model: String)
```

case classes automatically have equality and nice toString methods based on the constructor arguments.

```scala
val c1 = Calculator("HP","20b")
val c2 = Calculator("Casio","23")
c1 == c2

def calcType(calc: Calculator) = calc match {
  case Calculator("HP", "20B") => "financial"
  case Calculator("HP", "48G") => "scientific"
  case Calculator("HP", "30B") => "business"
  case Calculator(ourBrand, ourModel) => "Calculator: %s %s is of unknown type".format(ourBrand, ourModel)
}


case Calculator(_, _) => "Calculator of unknown type"
```

case classes can have methods just like normal classes.



# static in scala

In Scala there are no static methods: all methods are defined over an object:
- the method belongs to an instance of a class
- the method belongs to a singleton

static members in Java are modeled as ordinary members of a companion object in Scala.

When using a companion object from Java code, the members will be defined in a companion class with a static modifier. This is called static forwarding. It occurs even if you haven’t defined a companion class yourself.









# exceptions in scala

```
try {
  //
} catch {
  case e: ServerIsDownException => log.error(e, "the remote calculator service is unavailable. should have kept your trusty HP.")
} finally {
  remoteCalculatorService.close()
}
```


# Flow Controls statements


- if

```scala
if ( n == 5 ){
	println("n == 5 true")
} else if (n == 6) {
	println("n == 6 true")
} else {
	println("other case")
}
```

- ternary operator

```scala
if (k == 10) "k >= 10" else "k <> 10"
println(if (k == 10) "k == 10" else "k <> 10")

def is_ten(k: Int): String = if (k == 10) "k >= 10" else "k <> 10"
```
- match (non-patter-matching)


```scala
val month = 12

month match {
	case 1 => "January"
	case 2 => "February"
	case 12 => "December"
}

println( month match {
	case 1 => "January"
	case 2 => "February"
	case 12 => "December"
})

val mont = 13

month match {
	case 1 => "January"
	case 2 => "February"
	case 12 => "December"
	case _ => "none"
}

```


- loops


```scala
var k = 0
while (k<20){
	println("k="+k)
	k=k+1
}

// better with interpolation
var k = 0
while (k<20){
	println(s"k=$k")
	println(s"k=${k}")
	k=k+1
}


do {
	k=k-1
	println(s"k=$k")
} while (k>0)


// for

```scala
val lang = Seq("java","scala","kotlin","ruby")
for (l => println(s"$1 is cool"))

for (l <- lang){
	println(s"$1 rules!")
}


val opinions = Seq("cool", "boring")
for (l <- lang; o <- opinions){
	println(s"$1 is $o")
}
```



// forEach





```scala

```











# generics

like "java generics" or "c++ templates"

```scala
abstract class MyList[T] {
	def head: T
	def tail: MyList[T]
}


val aList: List[Int] = List(1,2,3)
val first: aList.head
```















# collections

  + collections inmutables
  + collections mutable


```
hierarchy of collections

               Traversable
                    |
                 Iterable
--------------------------------------------
      Set         Map                 Seq
                            ------------------------
                            IndexedSeq     LinearSeq
```




```scala
import scala.collection.inmutable
import scala.collection.inmutable._
import scala.collection.inmutable.{Set,ListMap}
import scala.collection.mutable
object Worksheet {

	val fruits = Array("apple","orange")
	val other = Array("apple","orange",6)
	// Array[Any] = Array(apple, orange, 6, true)
	val another = Array("apple","orange",6,true)
	// another: Array[Any] = Array(apple, orange, 6, true)


	fruits.apply(1)   // res3: String = orange
	fruits(1)         // res3: String = orange
	fruits.isEmpty
	fruits.nonEmpty
	fruits.map{ (x: String) => x.length}
	fruits.map{ _.length }

	val set = Set(1,2,3)
	set.contains(3)
	set.contains(4)
	set contains 4

	set + 4
	set ++ Set(5,6,7)
	set - 1
	set -- Set(1)

	set |   // union
	set &   // intersection
	set &~  // diference


	val mset = mutable.Set(1,2,3)
	mset + 4
	mset += 4
	mset - 2
	mset -= 2
	mset
	mset.retain{ x => x % 2 == 0} // like filter

	mset ++= Set(4,5)
}
```



# pseudo-collections: Option, Try

pseudo-collection solve the problem about ckeck nullity like

```c++
value = methodWhichCanReturnNull();

if(value == null){
	// defensive code
}
```



option is a collection which contains at mos one element Some(value) or None

```scala
def methodWhichCanReturnNull(): String = { "hello scala" }

val anOption = Option(methodWhichCanReturnNull()) // Some("hello scala")

val stringProcessing = anOption match {
	case Some(msg) => s"valid string $msg"
	case None => ""
}
```

also it can use with exceptions

```scala
def methodWhichCanReturnNull(): String = throw new RuntimeException
try {
	methodWhichCanReturnNull()
} catch {
	case e: Exception => "defend against exception"
}


val anotherStringProcessing = aTry match {
	case Success(validValue) => "I have obtained a valid string"
	case Failure(ex)         => "I have obtained an exception"
}
```




# advanced functional

## lazy evaluation

```scala
val aNonLazyValue = {
	println("executed")
	2
}
// executed
// aNonLazyValue: Int = 2

aNonLazyValue+1
//res4: Int = 3





lazy val aLazyValue = {
	println("executed")
	2
}

aLazyValue+1
// executed
// res3: Int = 3

```


## Futures

evaluate something into another thread. a future is a collection which contains a value when it's evaluated

a future is composable with map, flatmap, filter
monad

```scala
import scala.concurrent.ExecutionContent.Implicits.global // like a thread pool

val aFuture = Future({
	println("loading...")
	Thread.sleep(1000)
	println("done")
	42
})

Thread.sleep(2000)
```


## implicits

there are two common use cases for using implicits:

1. implicits arguments


```scala
def aMethodWithImplicitArgs(implicit arg: Int) = arg + 1
implicit val myImplicit = 46

println(aMethodWithImplicitArgs)
```

2. implicits class conversions

```scala
implicit class MyRichInteger(n: Int){
	def isEven(): Boolean = n % 2 == 0
}

println(23.isEven())
```


## pattern matching

pattern matching can use like a switch and like the switch the orden is important



a simple, value based pattern matching

```scala
val x: Int = 42
val order =  x match {
	case 1 => "1nd"
	case 2 => "2nd"
	case 3 => "3nd"
	case _ => s"${x}nd"
}

println(order)
```

pattern maching can deconstruct:
- case clasess
- tuples
- list

```scala
case class Person(name: String, age: Int)
val bob = Person("Bob",43)

val personGreeting = bob match {
	case Person(n,y) => s"$n, $y years"
	case _           => s"person schema bad formed"
}
```

```scala
val values = (0,1,2,3)

val problem = values match {
	case values(0,_,_,_) => " first component zero"
	case values(_,0,_,_) => " second component zero"
	case values(_,_,0,_) => " third component zero"
	case values(_,_,_,0) => " four component zero"
	case values(_,_,_,0) => " not problem"
}
```


```scala
val values = List(0,1,2,3)

val problem = values match {
	case List(_)   => " size 1"
	case List(_,_) => " size 2 "
	case List(_) => " wathever"
}
```



## High Order Functions

 + map
 + flatten
 + flapMap
 + filter
 + fold