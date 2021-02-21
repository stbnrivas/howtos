# TODO

## case classes, 2009 explanation

Scala supports the notion of case classes. Case classes are regular classes which export their constructor parameters and which provide a recursive decomposition mechanism via pattern matching.


```scala
abstract class Term
case class Var(name: String) extends Term
case class Fun(arg: String, body: Term) extends Term
case class App(f: Term, v: Term) extends Term


Fun("x", Fun("y", App(Var("x"), Var("y"))))
```

- The constructor parameters of case classes are treated as public values and can be accessed directly.

- For every case class the Scala compiler generates equals method which implements structural equality and atoString method. For instance


- It makes only sense to define case classes if pattern matching is used to decompose data structures. The following object defines a pretty printer function for our lambda calculus representation:

```scala
  def printTerm(term: Term) {
    term match {
      case Var(n) =>
        print(n)
      case Fun(x, b) =>
        print("^" + x + ".")
        printTerm(b)
      case App(f, v) =>
        Console.print("(")
        printTerm(f)
        print(" ")
        printTerm(v)
        print(")")
    }
  }
```

## case classes, 2020 explanation

In Scala, case classes are used to represent structural data types. They implicitly equip the class with meaningful `toString`, `equals` and `hashCode` methods, as well as the ability to be deconstructed with pattern matching.


In this example, we define a small set of case classes that represent binary trees of integers (the generic version is omitted for simplicity here). In inOrder, the match construct chooses the right branch, depending on the type of t, and at the same time deconstructs the arguments of a Node. 


```scala
// Define a set of case classes for representing binary trees.
sealed abstract class Tree
case class Node(elem: Int, left: Tree, right: Tree) extends Tree
case object Leaf extends Tree

// Return the in-order traversal sequence of a given tree.
def inOrder(t: Tree): List[Int] = t match {
  case Node(e, l, r) => inOrder(l) ::: List(e) ::: inOrder(r)
  case Leaf          => List()
}
```


## traits 

- traits into traits

- traits into classes