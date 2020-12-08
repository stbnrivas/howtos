# gnu make

The make program is intend to automate the mundane aspects of transforming source code into an executable

Make defines language for describing teh relationships between source code, intermediate files and executables.

The advantages of make is that you can specify the relations between the elements of your program , and mek it knows what steps need to be redone to produce a fresh compilation without redo all steps.

The compilation process is about a graph of dependences, remember make firs analizyes an entire makefile to build a dependency tree to build the desired targets. A makefile also contain comments, variable assgnments, macro definition, directives and conditional directives..

To make an executable program, we need to link compiled object files. and to generate object files we need a sources files

```c
// hello.c
#include <stdio.h>

int main(int argc, char* argv[]){
	printf("hello world");
}
```

```bash
# gcc and cc can Compile and Link Separately

# compiling only option with -c it gives a => hello.o
cc -c hello.h hello.c

# compiling and linking into single step
cc -o main file1.h file.cpp

# linking split steps
cc -c file1.c
cc -c file2.c
cc -o main file1.o file2.o

# additionally can add -g which generates additional symbolic debuggging information for use with gdb debugger
cc -g hello.o -o hello

# compiling with including dependences
cc hello.c -o hello.o -I/home/user/lib/

# Searching for Header Files and Libraries (-I, -L and -l)
# - static lib : A static library has file extension of ".a"
# - shared lib: A shared library has file extension of ".so" (shared objects)

# The include-paths are specified via -Idir option (or environment variable CPATH). Since the header's filename is known (e.g., iostream.h, stdio.h), the compiler only needs the directories

# The linker searches the so-called library-paths for libraries needed to link the program into an executable. The library-path is specified via -Ldir option (uppercase 'L' followed by the directory path) (or environment variable LIBRARY_PATH). In addition, you also have to specify the library name. In Unixes, the library libxxx.a is specified via -lxxx option (lowercase letter 'l', without the prefix "lib" and ".a" extension). In Windows, provide the full name such as -lxxx.lib. The linker needs to know both the directories as well as the library names. Hence, two options need to be specified.

# Default Include-paths, Library-paths and Libraries
# pre processor
cpp -v

cc -v

```




## targets, dependencies and commands

```makefile
# sintax
# target: dependence, dependence
# 	command1
# 	command2
# 	command3

hello: hello.c
	cc hello.c -o hello
```

```bash
make 
# or you can build specific target
make hello

make -f specific-makefile
```

typically the default goal in most makefiles is to build a program. Often the source code for the programs is incomplete and must be generated using utilities as flex or bison ( tooling for compilers buildings )

- flex: (fast lexical analizers) generate c code
- bison: a general-purpose parser generator that converts a grammar description


```c
#include <stdio.h>

extern int fee_count, fie_count, foe_count, fum_count;
extern int yylex(void);

int main(int argc, char *argv[]){
	yylex();
	printf("%d%d%d%d\n",fee_count, fie_count, foe_count, fum_count);
	exit(0);
}
```

```makefile
# `-l` a library named fl => libfl.a it is sintax make not gcc
count_words: count_workds.o lexer.o -lfl
	gcc count_workds.o lexer.o -lfl -o count_words
count_words.o: count_works.c
	gcc count_words.c
lexer.o: lexer.c
	gcc lexer.c
lexer.c lexer.l
	flex -t lexer.l > lexer.c
```

```bash
make 
```
- makefile accepts variables like this

```
${}
$()
```

- makefile has a predefined variables

```
$@     the filename of the target
$%     the filename element of an archive member specification
$<     the filename of the first prerequisite
$?     the names of all prerequisites tha are newer than the target, separated by spaces
$^     the filename of all the prerequisites separated by spaces, without duplicated
$+     similar to $^ but without prerequisites
$*     the stem of the target filename (stem a filename without suffix)
# because compatibility 
$(@D)  
```

- makefile accepts wildcards, also known as globbing are identical to bash

`~,*,?,[][^]`
[a-z]
[^a-z]

```makefile
prog: *.c
	$(CC) -o $@ $^
```

- also can clean, clean it's not into graph of compilation

```makefile
clean: 
	rm -f *.o temporary.o
```


-  using traditional source tree layout 

```
tree -L 2

.
└── Project
    ├── include
    └── src
```

## rules

```makefile
CC = gcc
CFLAGS = -Wall -g -std=c99
LDFLAGS = -lm                # where are libraries to link with
                             # for example:
                             # -lm  libm.so linked (the math lib)
                             # -lscandir  will link (libscandir.a)

main: 
	$(CC) $(CFLAGS) $(OBJECTS) -o main $(LDFLAGS)
```


## simple toy makefile

```c
// cool.h
#include <stdio.h>
#ifndef _COOL_H_
#define _COOL_H_

int cool();
#endif


// cool.c
#include "cool.h"
int cool(){
	printf("coool!!");
}


// main.c
#include "cool.h"

int main(){
	cool();
}
```

```makefile
main: main.c cool.o
	cc main.c -o main cool.o

cool.o: cool.h cool.c
	cc -c cool.c -o cool.o
```


## a makefile with system libraries TODO

```c
// cool.h
#include <stdio.h>
#include <math.h>
#ifndef _COOL_H_
#define _COOL_H_

int cool();
#endif


// cool.c
#include "cool.h"
int cool(){
	printf("coool!! x%d",pow(2,3));
}


// main.c
#include "cool.h"

int main(){
	cool();
}
```

```makefile
main: main.c cool.o
	cc main.c -o main cool.o

cool.o: cool.h cool.c
	cc -c cool.c -o cool.o
```


## a real makefile

```makefile
CC=cc
CFLAGS=-Wall -g -std=c99
LDFLAGS=-lm

%.o: %.c
	$(CC) $(CFLAGS) -o $@ -c $<
```

## makefile like a pro


```makefile
### If you wish to use extra libraries (math.h for instance),
### add their flags here (-lm in our case) in the "LIBS" variable.

LIBS = -lm

###
CFLAGS  = -std=c99
CFLAGS += -g
CFLAGS += -Wall
CFLAGS += -Wextra
CFLAGS += -pedantic
CFLAGS += -Werror
CFLAGS += -Wmissing-declarations
CFLAGS += -DUNITY_SUPPORT_64

ASANFLAGS  = -fsanitize=address
ASANFLAGS += -fno-common
ASANFLAGS += -fno-omit-frame-pointer

test: tests.out
	@./tests.out

memcheck: test/*.c src/*.c src/*.h
	@echo Compiling $@
	@$(CC) $(ASANFLAGS) $(CFLAGS) src/*.c test/vendor/unity.c test/*.c -o memcheck.out $(LIBS)
	@./memcheck.out
	@echo "Memory check passed"

clean:
	rm -rf *.o *.out *.out.dSYM

tests.out: test/*.c src/*.c src/*.h
	@echo Compiling $@
	@$(CC) $(CFLAGS) src/*.c test/vendor/unity.c test/*.c -o tests.out $(LIBS)
```



## dependencies

