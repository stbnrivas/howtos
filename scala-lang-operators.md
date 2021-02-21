# scala operators

- scala allow re-implementing your own operators and building DSL, also the methods `apply`, `update`, `unapply`. Also scala has
dynami invocations, the method calls can be intercepted at runtime


- scala has alphanumeric, operator character, unary and binary, 


## identifiers

the names of variables, functions, classes ar called identifiers

- operator characters ! # % & * + - / : < = > ? @ \ ^ | ~ 
- unicode mathematical symbols


## infix operators


```scala
1 to 10
1.to(10)

1 -> 10
1.->(10)

class Fraction(up: Int, down: Int) {
	def /(): String = s"$up/$down"
}

val f: Fraction = new Fraction(1,2)
f/
```


## unary operators

a identfier
42 toString