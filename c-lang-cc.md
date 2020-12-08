# compilers

GCC originally "GNU C Compiler" has grown to support other languages and has been redefined as "GNU Compiler Collection"

- gcc c compiler (GNU Compiler Collection)
- g++ c++ compiler (from gcc)
- cc (C Compiler)

It depends of the platform,  on linux probably cc will be a link to gcc, on solaris cc is sun c compiler


```bash
whereis gcc
whereis cc
diff /usr/bin/gcc /usr/bin/cc
```



# cc

```bash
# -Wall => Warnings all
# -o    => output file
cc -Wall circle.h -o circle
```

file types use extension for

```
*.h   header files
*.c   source files
*.i   preprocessor files
*.s   assembly files
*.S   assembly files with preprocesor directives before assembling
```


## preprocessing

```bash
# -E stop after preprocessing
# -o
# -C include comments
gcc -E -o main.i main.c

# -D name[=definition]  define a symbol used with #ifdef conditional compiling
# -U name               undefine a symbol used with #ifdef conditional compiling

#ifdef
#else
#endif

gcc -E -C -D _DEBUG_ -o main.i main.c

# -iquote specify a directory to get header in quotation marks, not angle brackets
# -i[directory:[]]
gcc -i includes -E main.i -o main

# -system
```


```
flag to search required include into specific directories
-I directory[:directory[]]

```

## assembly

not real assembly, it is RTL (register transer language)

```bash
# -S stop after build assembly
gcc -S main.c -o main.rtl
```

## compilation only

```bash
# only compile but don't link to executable
gcc -c example.h example.c -o example.o
```



## linking

the linker joins a number of binary object files into a singel executable file. the linker must add also teh code for any C standard library functions. A library is simply a sert fo object files collected in a single archiver file.

the bulk of the standard library functions are ordinarily in teh file libc.a (the ends `.a` is for archive) or a shared library for dynamic linking libc.so (the ends `.so` is for shared object)

Also you can use `ar`  ar is considered a binary utility because archives of this sort are most often used as libraries holding commonly needed subroutines.



```c
#include <curses.h>

int main(){
	(void) initscr();
	keypad(stdscr, TRUE);
	(void) nonl();
	(void) cbreak;
	printw("from ncurses, press any key to exit");
	getch();
	endwin();
	return 0;
}
```

```bash
# -l ncurses: search for libncurses.so in linux into
# /usr/lib
# /usr/local/lib/
gcc -o main main.c -l ncurses
```

- dinamic linking and shared object files

shared libraries are special object files that cna be linked to a program at runtime. The use of shared libraries has a number of advantages: a programs's executable file ise smaller adn shared modules permit modular updating, as well as more efficient use of the available memory, to create a shared obje file use `-shared` flag

```c
// cool.h
#include <stdio.h>

int cool();

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


```bash
gcc -c cool.c                     # compile
gcc -c cool.c -o cool.o           # equivalent

gcc cool.o -shared -o libcool.so  # create a shared object

gcc main.c -o main libcool.so     # build executable
gcc main2.c -o main2 libcool.so

# error while loading shared libraries: libcool.so: cannot open shared object file: No such file or directory



gcc -static -o main main.c cool.o
gcc -static -o main2 main2.c cool.o
```


## c dialects

```bash
gcc -ansi  # disable all gcc extensions

gcc -std=iso9899:1990 # equivalents
gcc -std=c90
gcc -std=c89


gcc -std=c99
gcc -std=c11
```


## compilation error warnings

```bash
gcc -w        # disable all warnings
gcc -pedantic # show the warnings
gcc -Wall     # show the warnings
gcc -Wextra   # show legal but questionable
gcc -W
```


## Optimization

every level of optimization represents a number of optimization tecniques and the level are cumulative.

```bash
gcc -O0

gcc -O1

gcc -O2

gcc -O3

gcc -Os
```

## Debugging

use `-g` to include symbol and source info to debug


use `-p` to add special function to your program to outpu profiling information when you run it