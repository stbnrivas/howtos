# Maven

## installation linux





## installation windows 10

```
M2_HOME=C:\MAVEN\apache-maven-3.6\
MAVEN_HOME=C:\MAVEN\apache-maven-3.6\

PATH=PATH;%M2_HOME%
```


## using maven


```bash
mvn -v
mvn --help

# usage: mvn [options] [<goal(s)>] [<phase(s)>]
...
```

```bash
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false

# for windows 10 needs surround with quotes
mvn archetype:generate "-DgroupId=com.mycompany.app" "-DartifactId=my-app" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DarchetypeVersion=1.4" "-DinteractiveMode=false"

cd my-app
```

you can use diferents archtypeArtifactId

```bash
maven-archetype-archetype       An archetype to generate a sample archetype project.
maven-archetype-j2ee-simple     An archetype to generate a simplifed sample J2EE application.
maven-archetype-mojo            An archetype to generate a sample a sample Maven plugin.
maven-archetype-plugin          An archetype to generate a sample Maven plugin.
maven-archetype-plugin-site     An archetype to generate a sample Maven plugin site.
maven-archetype-portlet         An archetype to generate a sample JSR-268 Portlet.
maven-archetype-quickstart      An archetype to generate a sample Maven project.
maven-archetype-simple          An archetype to generate a simple Maven project.
maven-archetype-site            An archetype to generate a sample Maven site which demonstrates some of the supported document types like APT, XDoc, and FML and demonstrates how to i18n your site.
maven-archetype-site-simple     An archetype to generate a sample Maven site.
maven-archetype-webapp          An archetype to generate a sample Maven Webapp project.


TEMPLATE=maven-archetype-quickstart
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=${TEMPLATE} -DarchetypeVersion=1.4 -DinteractiveMode=false
```




```bash
# only compile
mvn compile
# build and create jar or war
mvn package
# clean build at target folder
mvn clean
# 
mvn verify
```

execute


```bash
cd target


artifact=my-app-1.0-SNAPSHOT.jar
main_class=com.mycompany.app.App
java -cp ${artifact} 

```


configuration at pom.xml



By default your version of Maven might use an old version of the maven-compiler-plugin that is not compatible with Java 9 or later versions. To target Java 9 or later, you should at least use version 3.6.0 of the maven-compiler-plugin and set the maven.compiler.release property to the Java release you are targetting (e.g. 9, 10, 11, 12, etc.).



Maven Phases

Although hardly a comprehensive list, these are the most common default lifecycle phases executed.

    validate: validate the project is correct and all necessary information is available
    compile: compile the source code of the project
    test: test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
    package: take the compiled code and package it in its distributable format, such as a JAR.
    integration-test: process and deploy the package if necessary into an environment where integration tests can be run
    verify: run any checks to verify the package is valid and meets quality criteria
    install: install the package into the local repository, for use as a dependency in other projects locally
    deploy: done in an integration or release environment, copies the final package to the remote repository for sharing with other developers and projects.

There are two other Maven lifecycles of note beyond the default list above. They are

    clean: cleans up artifacts created by prior builds

    site: generates site documentation for this project




search dependencies at [https://mvnrepository.com/](https://mvnrepository.com/) and add as dependency into pom.xml

```xml
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.21</version>
</dependency>
```