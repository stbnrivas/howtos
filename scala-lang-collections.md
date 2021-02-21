# scala collections

- all collections in scala extends the Iterable trait
- the biggest categories of collections are sequences, sets, maps
- scala has mutable immutable versions
- `+`  add an element to an unordered colection
- `+:` `:+` prepend or append to a sequence
- `++` concatenates two collections
- `-`  `--` remove elements
- `map` `fold` `foldLeft` `foldRight` `zipping` are available
- immutable collections never change so can share even mulltithreaded program


scala support mutable and immutable collection, the key to work with immutable collections is that yoyu create new collections our of old ones.

```
               Iterable<<trait>>
                     |
                     |
                     |
    ---------------------------------
    |                |              |
<<trait>>        <<trait>>      <<trait>>
   Seq              Set            Map
    |                |              |
<<trait>>         <<trait>>     <<trait>>
IndexedSeq        SortedSet     SortedMap

```


```scala
val a1 = Array(1,2,3)
val iter = a1.iterator

while(iter.hasNext) { println(iter.next()) }

for (e <- a1) println(e)
```

each scala collection trait has a companion object with an apply method for constructing an instance of the collection. because *The uniform creation principle*

```scala
scala.collection.immutable.Iterable(0,1,2,3)
scala.collection.immutable.Set(0,1,2,3)
scala.collection.immutable.Map(0,1,2,3)
scala.collection.immutable.SortedSet(0,1,2,3)

scala.collection.mutable.Iterable(0,1,2,3)
scala.collection.mutable.Set(0,1,2,3)
scala.collection.mutable.Map(0,1,2,3)
scala.collection.mutable.SortedSet(0,1,2,3)
```

Also there are methods toSeq, toSet, ToMap and so on, as well as a generic `to[C]` method that you can use to 
translate between collection types

```scala
val a1 = Array(1,2,3)

a1.to[Seq]
a1.to[Set]

val a2 = Array((1,"one"),(2,"two"),(3,"three"))
a2.toMap
a2.to[Map[Int,String]] // error
```



## list 

```scala
val digits = List(4,2)
4 :: List(2)
4 :: 5 :: 2 :: Nil
```

in scala you can use recursion the naturally

```scala
def sum(l: List[Int]): Int = if (l==Nil) 0 else l.head + sum(l.tail)

sum( 1 :: Nil)

def sum(l: List[Int]): Int = l match {
	case Nil => 0
	case h :: t => h + sum(t) 
}
sum( 1 :: 2 :: 3:: Nil)
```

## set

it don't have repeated elements

```scala
val s = Set(42,0,1,5)
```

- a LinkedHashSet remember the order


```scala
val even = Set(1,3,5)
val odd = Set(0,2,4)
```




## methods



```scala
val buf = scala.collection.mutable.ArrayBuffer
val buf = scala.collection.mutable.ListBuffer.empty[Int]
val buf = new StringBuilder


var h = new HashMap()
val map = scala.collection.mutable.Map[Int,String]()
```