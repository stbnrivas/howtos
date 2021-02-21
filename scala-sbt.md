# scala-sbt.md

[https://github.com/shekhargulati/52-technologies-in-2016/blob/master/02-sbt/README.md](https://github.com/shekhargulati/52-technologies-in-2016/blob/master/02-sbt/README.md)

- sbt (scala build tool)
- sbt into scala project is a interactive tool
- all terminology in sbt consist in tasks (something to perform like compile) and settings (a value)
- the task can depend on another task todo its job, sbt create a dependency graph to can running parallel
- the taks compile is a dependency of task run 
- sbt can run in two modes
  + command line like `sbt compile` or `sbt about`
  + interactive mode running `sbt` like a REPL

- By default, sbt follows Maven project layout i.e. Scala source files are placed inside src/main/scala and test source files are placed inside src/test/scala

```
This is a list of tasks defined for the current project.
It does not list the scopes the tasks are defined in; use the 'inspect' command for that.
Tasks produce values.  Use the 'show' command to run the task and print the resulting value.

  clean            Deletes files produced by the build, such as generated sources, compiled classes, and task caches.
  compile          Compiles sources.
  console          Starts the Scala interpreter with the project classes on the classpath.
  consoleProject   Starts the Scala interpreter with the sbt and the build definition on the classpath and useful imports.
  consoleQuick     Starts the Scala interpreter with the project dependencies on the classpath.
  copyResources    Copies resources to the output directory.
  doc              Generates API documentation.
  package          Produces the main artifact, such as a binary jar.  This is typically an alias for the task that actually does the packaging.
  packageBin       Produces a main artifact, such as a binary jar.
  packageDoc       Produces a documentation artifact, such as a jar containing API documentation.
  packageSrc       Produces a source artifact, such as a jar containing sources and resources.
  publish          Publishes artifacts to a repository.
  publishLocal     Publishes artifacts to the local Ivy repository.
  publishM2        Publishes artifacts to the local Maven repository.
  run              Runs a main class, passing along arguments provided on the command line.
  runMain          Runs the main class selected by the first argument, passing the remaining arguments to the main method.
  submit           submit
  submitLocal      submit local to a given file path
  test             Executes all tests.
  testOnly         Executes the tests provided as arguments or all tests if no arguments are provided.
  testQuick        Executes the tests that either failed before, were not run or whose transitive dependencies changed, among those provided as arguments.
  update           Resolves and optionally retrieves dependencies, producing a report.

More tasks may be viewed by increasing verbosity.  See 'help tasks'.
```


```bash
# create a project from a template (g8 giter8 templete system )
sbt new sbt/scala-seed.g8

# other templates
# sbt new foundweekends/giter8.g8 (A template for Giter8 templates)
# sbt new scala/scala-seed.g8 (Seed template for Scala)
# sbt new scala/hello-world.g8 (A template to demonstrate a minimal Scala application)
# sbt new scala/scalatest-example.g8 (A template for trying out ScalaTest)
# sbt new akka/akka-scala-seed.g8 (A minimal seed template for an Akka with Scala build )
# sbt new akka/akka-java-seed.g8 (A minimal seed template for an Akka in Java )
# sbt new playframework/play-scala-seed.g8 (Play Scala Seed Template)
# sbt new playframework/play-java-seed.g8 (Play Java Seed template)
# sbt new lagom/lagom-scala.g8 (A Lagom Scala seed template for sbt)
# sbt new lagom/lagom-java.g8 (A Lagom Java seed template for sbt)
# sbt new scala-native/scala-native.g8 (Scala Native)
# sbt new scala-native/sbt-crossproject.g8 (sbt-crosspoject)
# sbt new http4s/http4s.g8 (http4s services)
# sbt new unfiltered/unfiltered.g8 (Unfiltered application)
# sbt new scalatra/scalatra-sbt.g8 (Basic Scalatra template using SBT 0.13.x.) 


# give a name for project 
# name [Scala Seed Project]: example

# cd appname
cd ${project}

# compile and execute
sbt
# First time you run sbt, it will download some jars that are required by sbt to perform its job. 

run

test

test-failed 

test-quick

exit

sbt tasks

clean 
```
into the sbt interactive tool

```bash
sbt
run
show name
show scalaVersion
show version
show organization

set organization := "com.boringcompany"
set scalaVersion := "2.13.1"

compile
reload
console


exit

# without interactive 

sbt compile                                  # compiles project
sbt run                                      # runs your program
sbt sbtVersion                               # displays sbt version
sbt console                                  # opens REPL console
sbt clean                                    # clean
sbt "test-only org.yourcompany.YourTestSpec" # runs a single test
sbt test                                     # runs every tests
sbt ";clean ;compile; run"                   # combines multiple commands in a single invocation
```



all projects in scala should have a build.sbt

```
sbt.version=0.13.16

libraryDependencies += "org.scalatest" % "scalatest_2.11" % "2.2.6" % "test"

# libraryDependencies += groupID % artifactID % version % configuration

libraryDependences ++= Seq(
	"joda-time" % "joda-time" % "2.9.2"
	"org.joda" % "joda-converte" % "1.8"
)


scalacOptions ++= Seq("-feature", "-language:_", "-unchecked", "-deprecation", "-encoding", "utf8")
```


## writing your own task


- You have to define a TaskKey for your task
- You have to provide the task definition

```
val gitCommitCountTask = taskKey[String]("Prints commit count of the current branch")


gitCommitCountTask := {
  val branch = scala.sys.process.Process("git symbolic-ref -q HEAD").lines.head.replace("refs/heads/","")
  val commitCount = scala.sys.process.Process(s"git rev-list --count $branch").lines.head
  println(s"total number of commits on [$branch]: $commitCount")
  commitCount
}
```


```bash
sbt gitCommitCountTask
```

A skeleton SBT project

```
/project-root
|_src
   |_main
      |_scala
      |_java
      |_resources
   |_test
      |_scala
      |_java
      |_resources
|_project
   |_plugins.sbt
   |_build.properties
   |_Build.scala
|_target
build.sbt
```