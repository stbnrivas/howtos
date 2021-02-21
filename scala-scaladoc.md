# yet scaladoc needs to be deciphering



`def count(p: (A) => Boolean): Int`

count takes de predicate p, that it is a function from A to Boolean and return an Int

`def append(elems: A*): Unit` 

append take elems (zero or more argument of type A) and return Unit (void)


`def appendAll(xs: TraversableOnce[A]): Unit`  

appendAll take any collection which are TraversableOnce trait and return Unit


`def containsSlice[B](that: GenSeq[B]): Boolean`

containsSlice declare to use a type B
containsSlice takes that which is a GenSeq (a collection sequential) of elements type B and return boolean

`def +=(elem: A): ArrayBuffer.this.type` 

+= takes elem of type A and return this which allows you to chain calls, `b += 4 += 1`

`def copyToArray[B >: A](xs: Array[B]): Unit`

copyToArray declare a types B, A which  B is supertype of A. you can copy ArrayBuffer[Int] to Array[Any]

`def sorted[B >: A](implicit cmp: Ordering[B]): ArrayBuffer[A]`

sorted declare B is supertype of A
sorted takes comp as implicit param which has a trait Ordering of type B and return ArrayBuffer of A

`def ++:[B >: A, That](that: collection.Traversable[B])(implicit bf: CanBuildFrom[ArrayBuffer[A], B, That]): That`


