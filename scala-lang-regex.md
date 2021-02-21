# regex in scala

`scala.util.matching.Regex`


```scala
val numPattern = "[0-9]+".r

// to avoid scape backslashes, quotation ... use raw

val difficultPattern = """\s+[0-9]+\s""".r


for (matchString <- numPattern.findAllIn("99 bottles of beer, 98 bottles ...")){
	println(matchString)
}

val matches = numPattern.findAllIn("99 bottles of beer, 98 bottles ...").toArray


val fistMatch = numPattern.findFirstIn("99 bottles of beer, 98 bottles ...")

numPattern.replaceFirstIn("99 bottles of beer, 98 bottles ...","X")

numPattern.replaceAllIn("99 bottles of beer, 98 bottles ...","X")
```
