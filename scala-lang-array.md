# working with arrays in scala

- use an Array if the length is fixed or ArrayBuffer if not

- scala and java arrays are interoperable with ArrayBuffer use scala.collection.

- don't use new when supplying initial values

- for(elem <- arr)





```scala
val a = Array[Int](1, 2, 3)
val nums = new Array[Int](100)              // unusable
val words = new Array[String](10)           //
val greetings = Array("hi","howdy","hello") // 
```

```scala
import scala.collection.mutable.ArrayBuffer

val a = ArrayBuffer[Int]()
val b = new ArrayBuffer[Int]
val c = new ArrayBuffer[Int]()

a += 1
a ++= Array(2,3)
a ++ ArrayBuffered(11,12,13,14)



val b = new scala.collection.mutable.ArrayBuffer[Int]()
b.insert(0,0)
b.insert(1,1)
b.insert(b.length,2)
for (i <- 0 until b.length) println(s"$i: ${b(i)}")

for (elem <- b) println(elem)

// returning other array
for (e <- b) yield e-1

// removing elements
var result =  for (e <- b if e > 0) yield e

b.sum
b.sorted
b.sortWith( _ < _ )
b.sortWith( _ > _ )
b.mkString(" and ")
b.mkString(",")
b.mkString("<",",",">")
```


```scala
var a = new Array(10)
a
// Array[Nothing] = Array(null, null, null, null, null, null, null, null, null, null)


var b = Array(10) //calls apply(10) setting an array with single element 10
b.length
// res16: Int = 1
```

# multidimensional arrays

are implemented as array of arrays


```scala
val a = Array.ofDim[String](rows, cols)

var triangles = new Array[Array[Int]](10)
triangles.insert(new Array(0,1,2))
```
