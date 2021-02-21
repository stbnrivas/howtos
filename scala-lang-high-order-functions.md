# scala high-order functions

A High Order function is a function tha does at least one of requirements

- takes one or moer function as arguments
- returns a function as its result

In scala the functions are first-class citizens that can be passed around just like other data types


```scala
import scala.math._
val num 3.14
val f1 = ceil _
val f2 = (_: String).charAt(_: Int)


f1(2.7182)    // 3.0
f2("abcde",0) // a

Array(3.14, 1.42, 2.0).map(f1)

// anonymous function
val t = (x: Integer) => 3 * x
t(1)

Array(3.14, 1.42, 2.0).map( (x: Double) => 3 * x )
Array(3.14, 1.42, 2.0).map{ (x: Double) => 3 * x }
```

- a function that takes another funcion as parameter

```scala
val identity = (d: Double) => 1.0
def half(f: (Double) => Double) = f(0.5)
half(identity)

def multiplier(f: (Double)=> Double, x: Double) = f(x)
multiplier(identity) // ERROR, cant return high order function
multiplier(identity, 3.5)


val multiplier2 = (f: (Double)=> Double, x: Double) => f(x)
multiplier2(identity) // ERROR, unspecified parameter 2
multiplier2(identity, 3.5)


// when type inference works you can ommission things to get 
// that nobody understand 
half( (x)=>(2*x) ) 
half( x=> 2*x)
half( 3*_ )
```

- useful high-Order functions

  + map
  + foreach (is like a map without return a value)
  + reduceLeft
  + filter  // 

```scala
(1 to 9).map(0.1 * _)
(1 to 9).map( (i: Int)=>i.toDouble*0.1 )

(1 to 9).map("*" * _).foreach(println _)

(1 to 9).filter( (Unit) => true )
```


## closures

A clousure consist of code together with the definitions of any nonlocal variable that the code uses.

In scala, you can define a function inside any scope: in a package, in a class, even another function or method. In the body of a function, you can access any variable from an enxlosing scope.

Note that your function may be called when the variable is no longer in scope

```scala
def mulBy(factor: Double) = (x: Double) => factor * x 
def mulBy(factor: Double) = { (x: Double) => factor * x }

val triple = mulBy(3) // the remain variables is popped off the runtime stack
val half = mulBy(0.2) // the remain variables is popped off the runtime stack

triple(1) // now arise remain variables
half(2)   // now arise remain variables



// let's try with more than one var
def sumAndDivBY(d: Double) = (x: Double, y: Double) => (x+y) / d

val divBy10 = sumAndDivBY(10.0)
divBy10(5,5)
```




# currying

Currying (named as Haskell Brooks Curry) is the process of turning a function that takes two arguments into a function taht takes one argument. That function returns a function that consumes teh second argument

```scala
val mul = (x: Int, y: Int) => x * y
val mulOneAtATime = (x: Int) => ((y: Int)=> x*y)
mulOneAtATime(2)(3)

// also can write
def mulCurrying(x: Int)(y: Int) = x * y
mulCurryin(1) // ERROR: missing argument list for method 
mulCurryin(1)(2)
```

currying are by all scaladoc like 

```
def method[B](that: Seq[B])(p: (A,B)=>Boolean): Boolean
```




