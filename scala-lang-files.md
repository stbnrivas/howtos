# files in scala

## reading lines

```scala
import scala.io.Source
val source = Source.fromFile("filenam.txt","UTF-8")
val lineIterator = source.getLines
for( l <- lineIterator) println(l)
source.close
```

```scala
val lines = source.getLines.toArray
val contents = source.mkString
```


## reading characters

```scala
import scala.io.Source
val source = Source.fromFile("filenam.txt","UTF-8")
for( c <- source) println(c)
source.close
```

## reading tokens (words)

```scala
import scala.io.Source
val source = Source.fromFile("filenam.txt","UTF-8")
val tokens = source.mkString.split("\\s+")
source.close
```

## reading from URL

```scala
import scala.io.Source
val source = Source.fromURL("https://www.scala-lang.org/api/","UTF-8")
// CAUTION fromURL you need to know the character set
source.close
```

## reading binary files

you need to use java library

```scala
val file = new File(filename)
val in = new FileInputStream(file)
val bytes = new Array[Byte](file.length.toInt)
in.read(bytes)
in.close
```


# writing files

you need to use java.io.PrintWriter 

```scala
val out = new PrintWriter("numbers.txt")
for (i <- 1 to 100) {
	// out.printf(i)
	out.print(f"$i%6d")
}
out.close
```



# directories

you need to use java.nio.file

```scala
import java.nio.file._
String dirname = s"/home/$user"
val entries = Files.walk(Paths.get(dirname)) 
try {
	entries.forEach(p=> println(p))
} finally {
	entries.close()
}
```