# hash map

- first you need to choose between mutable and immutable maps
- also tuples are useful for aggregatin values 
- never use `new`, is a traits.


```scala
val scores = Map("Alice" -> 10, "Bob" -> 3)
// scala.collection.immutable.Map[String,Int]

scores("Alice")
scores.contains("Bob")
scores.getOrElse("Bob",0)


# convert to fixed length
val other_scores = scores.withDefaultValue(0)
other_scores("ian")


val emptyMap: scala.collection.mutable.Map[String,Int] = scala.collection.mutable.Map()     
val initMap: scala.collection.mutable.Map[String,Int] = scala.collection.mutable.Map("wft" -> 1)     

initMap("two") = 2
initMap += ("three" -> 3, "four" -> 4) // deprecated
initMap ++= scala.collection.mutable.Map("three" -> 3, , "four" -> 4)


println(s"Elements of map2 = $map2")
```


iterating

```scala
val map: Map[Int,String] = Map(1-> "Junuary", 2-> "February")
for ((k,v) <- map) println(s"$k $v")

for ((k,v) <- map) yield v
for ((k,v) <- map) yield (v,k)
```


```scala
val sorted_scores = scala.collection.mutable.SortedMap("Alice"->10, "Ben"-> 0)
val linked_sorted_scores = scala.collection.mutable.LinkedHashMap("Alice"->10, "Ben"-> 0)
```