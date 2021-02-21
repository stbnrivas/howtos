# tuples in scala

the positions of tuple start with 1


```scala

Tuple2(1, "text")
Tuple3(1, "text", 1L)

// or simply
val coor = (1551.2,5541.5)

coor._1
coor._2


// like deserialization
val (long,_) = coor


val keys = Array(1,2,3)
val values = Array("one","two","three")
keys.zip(values).toMap
```