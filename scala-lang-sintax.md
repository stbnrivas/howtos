# scala language

Scala is a highly expressive and flexible language. highly sophisticated abstractions, so that library use


Scala embraces the functional programming style without abandoning object orienta-
tion, giving you an incremental learning path to a new paradigm.

semicolons are mostly optional

# scala installation

```bash
java -version
sbt about
```



# scala interpreter


```bash
scala
```

REPL (Read Evaluate Print Loop) because this is not interpreter, behind the scene code is compiled to bytecode


```scala
8*5
"hello world"
```

if you want to paste a block of code into REPL type

```
:paste
# `CTRL + D` to end
```


# Values and Variables

In scala, you are encouraged to use a val unless you really need to change the contents. The mutability is the evil.

Also you dont need specify the type of a value. It is inferred from expression. But specify is better

```scala
val greeting: String = null
res1: String = hello world
val greeting: String = "hello world"
// error: reassignment to val
```


# commonly used types

the void type is Unit

Byte, Char, Short, Int, Long, Float, Double, Boolean that are classes all in scala are object, no types primitives here..

```scala
1.toString()
1.to(10)
```

Also there are RichInt, RichDouble, RichChar... for convenience

Also BigInt, BigDecimal

Scala don't have cast, convert between numeric types 

```scala
1.0.toInt
```

arithmetic operartor overloading

```
+ - * / % 
& | ^ >> <<

a + b // shorthand for a.+(b)
```

scala *DON'T HAVE* ++ -- use +=1 -=1 remember mutate a integer value ... it does not sense


# methods calling

- if the method has not params, you dont have use parentheses


```scala
"Hello".sorted()
"Hello".sorted
```

- a parameterless method that doesn't modify the object has no parentheses

```scala
"Hello".intersect("World")
```

- scala don't have static methods, you should define such methods in singleton objects



- apply method, think on it as overladed method form of the () operator, because you should think like a function that map n position with their element

```scala
val s = "Hello"
s(0)
s(1)
s(2)
s(3)
s(4)
// conflict
"Bonjour".sorted(3)
"Bonjour".sorted.apply(3)
("Bonjour".sorted)(3)

```

- the methods can has function as parameters

- some method has implicit params

```scala
def sorted[B >: Char](implicit ord: math.Ordering[B]): String
// [B >: Char]  indecipherable incantation  any supertype of char
```

# val, var, def

- val is evaluated single time
- var is accessed every time
- def is evaluated every call



# control structures and functions


## conditional expresssions

`if` statement

```scala
val x = 0
if (x>0) 1 else -1
val s = if (x>0) 1 else -1 // common initialization

val p = if (x>0) 1 else "WTF!!" // common initialization
val q = if (x>0) 1 else () // return a unit

// multiline
if (x==0) { 
	0
} else if (x>1){
	1
} else {
	2
}
```

## block expressions and assignements

the value of the block { } is the last expression

```scala
val distance = { val dx = x - x0; val dy = y -y0; sqrt(dx*dx*dy*dy)}
```

In scala, assignmen tes have no value is Unit, as consecuence  a block that ends with an assignament as last expression return unit.


## string interpolation

strings are one of three predefined string interpolators in the scala library

- `s`   prefix, string can contain expressions but not format directives
- `raw` prefix, escape sequences in a strin are not evaluated 
- `f`   prefix, string can format 


## input and output

```scala
print("answer is 42")
print("answer is 42\n")

println("answer is 42")

val x: Integer = 42
printf("the answer is $x or ${21+21}","mmm",42)


println(f"$time | $logLevel%-5s | $classname | $msg\n")
/*
 info warn debug error ever have 5 spaces or fill, it does cool!!

04:52:51:541 | INFO  | Bar | this is an info message from class Bar
04:52:51:541 | WARN  | Bar | this is a warn message from class Bar
04:52:51:541 | DEBUG | Bar | this is an error message from class Bar
04:52:51:541 | ERROR | Baz | this is an error message from class Baz
*/
```



```scala
import scala.io

val name = scala.io.StdIn.readLine("Your name: ")
print("your age")
val age = scala.io.StdIn.readInt()
scala.io.StdIn.readDouble
scala.io.StdIn.readByte
scala.io.StdIn.readLong
scala.io.StdIn.readFloat
scala.io.StdIn.readBoolean
scala.io.StdIn.readChar
```

## Loops

```scala
while (n > 0) {
	r = r * n
	n -= 1
}
```

```scala
for (i <- 1 to n)
	r = r * 1

for (i <- 1 to 5){
	println(s"i= $i")
}

var sum: Int = 0
for (ch <- "hello") sum += ch
```

advanced loops

- multiples generators, cartessian product


```scala
for (i <- 1 to 3; j <- 1 to 3 ) println (s"$i + $j")
```


- with a guard

```scala
for (i <- 1 to 3; j <- 1 to 3 if i!=j) println (s"$i + $j")
```

- with a crazy var declaration into loop value..

```scala
for (i <- 1 to 3; from = 4 - i; j <- from to 3) println(f"$i%3d, $j%3d")
// Prints 13 22 23 31 32 33
```

- building a collection into loop (loop is called for comprehension)

```scala
for (i <- 1 to 10 ) yield i
// res0: IndexedSeq[Int] = Vector(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
```


## functions

In addition in scala we have functions, a method operate on an object but a function does not. 

```scala
def abs(x: Double) = if (x>=0) x else -x

def fact(n: Int) = {
	var r = 1
	for(i <- 1 to n) r = r * i
	r
}

def fact(n: Int):Int = {
	var r = 1
	for(i <- 1 to n) r = r * i
	r
}
```

When the function is recursive, you must specify return type, without it the compiler can not verify the type of return

```scala
def fact(n: Int): Int = if (n<=0) 1 else n*fact(n-1)
```

default arguments for a function

```scala
def decorate(str: String, left: String = "prefix", right: String = "suffix"): String = {
	left + str + right
}

decorate("-yeah-")
//res51: String = prefix-yeah-suffix

decorate("yeah","[","]")
//res52: String = [yeah]

decorate("yeah",right = "?")
//res54: String = [yeah=
```

function with a variable number of arg

```scala
def sum(args: Int*): Int = {
	var result = 0
	for (arg <- args) result += arg
	result
}
sum(0,1)
sum(0,1,2,3,4)
```

procedures (a function that return is Unit) omiting = symbol. this is very common error when the compiler complaint message "unit is not acceptable at that location"

```scala
def box(s: String) {
	printls("none is returned")
}
// or better explicitly
def box(s: String): Unit = {
	printls("none is returned")
}
```

## Enumerations

scala don't have enumerated types. but you can use `Enumeration` helper class

```scala
object TrafficColor extends Enumeration {
	val Red, Yellow, Green = Value
}

val red = TrafficColor.Red
```




##  lazy evaluation 

- lazy values, when a val is declarated as lazy its initialization is deferred until first accessd. laziness is not cost-free, every time is accessed a method is called in threadsafe


```scala
lazy val words = scala.io.Source.fromFile("/etc/..../file.txt")
```

## exceptions 


```scala
throw new IllegalArgumentException("x should not be negative")
```



## main function

every scala program must start with and object main method to be executed

```scala
object Hello {
	def main(args: Array[String]){
		println("hello world!!")
	}
}
```
or instead of privide a main, also you can extend the App trait and place the program code into 

```scala
object Hello extends App {
	println(s"hello $args")
}
```


## packages 

packages in scala are same that namespaces in C++ and java packages

- packages can be nested like inner classes
- packages path are not absolute, can be relative 
- A chain x.y.x leaves intermediate packages x and x.y without to be included

Every scala program has implicitly imported

```scala
import java.lang._
import scala._
import Predef._
```


- A package can contain classes, objects, and traits, but not definitions of functions or variables (JVM limitation)

```scala
// to force absolute path use
var s = _root_.scala.collection.mutable.ArrayBuffer
```


```scala
package com {
	package helper {
		package html{
			class Converter {

			}
		}
		package json{
			class Converter {

			}
		}
	}
}
```

```scala
package com.xxx
package folks
class Person {}

// equivalent to
package com.xxx {
	package folks {
		class Person {}
	}
}
```

visibility qualifiers ( private , protected) public doesn't exist

```scala
package com.xxx
package folks

class Person {
	private[folks] def test_into_folks = "not visible"
	
	//private[xxx] def test_into_xxx = "not visible"
	//private[com] def test_into_xxx = "not visible"
}
```

import * wildcard in scala are _


```scala
import java.awt.Color

import java.awt.Color._
val c1 = RED // Color.RED
val c2 = decode("#ff0000") // Color.decode

```


import can be anywhere 

```scala
class Manager {
	import scala.collection.mutable._
}
```


import more than one in single line


```scala
import java.aws.{Color, Font}
```

overlapping can hides previous importation

```scala
import java.util.HashMap
import scala.collection.mutable.HashMap

// solve renaming

import java.util.{HashMap => JavaHashMap}
import scala.collection.mutable.HashMap

```
