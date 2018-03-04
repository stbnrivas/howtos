# alternatives

alternatives - maintain symbolic links determining default commands


# changing java version

	$ alternatives --config java

	+  1        /usr/lib/jvm/jre-1.6.0-openjdk/bin/java
	*  2        /etc/alternatives/java_sdk/bin/java
	3           /usr/lib/jvm/jre-1.5.0-gcj/bin/java
	4           /usr/java/latest/bin/java
	5           /usr/java/jdk1.7.0/bin/java


	java --version
