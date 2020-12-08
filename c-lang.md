# c language


The procedural building block of a C program are functions. Every function in a well-designed program serves a specific purpose. 

The functions contain statements (declaration) for the program to execute sequentially.

Every C program must define at least one function with the special name `main()`, which is the first fucntion invoked when the program starts


Into C, the term identifier refers to the names of variables, funcitons, macros, structures and otehr objects defined into C program.

The scope of an identifier refers to a part of programs that can "see" that identifier. The type of scope is always determined by the location at which you declare the identifiers

- file scope

if you declare an identifier outside all blocks and parameter lists, the it has a file scope. You can use anywhere after the delaration and up to the end

- block scope

except for labesl, identifiers declared within a block have block scope. You can use such an identifier only from its declaration to the end of the smallest block containing that declaration. 

- function prototype scope

the parameter names in a function prototype have function prototype scope

- function scope

```c
// main.c
int x1 = 0;                // x var has file scope
int math_example(int x2);  // param x has a function prototype scope
int main(int argc, int *argv[]){
	int x3 = 1;
	if (x3 == 1){
		int x4 = 10; // x4 has a block scope
	}
}

int math_example(int x2){
	int factor = 2; // factor has function scope
	return x2 *2;
}

```

- declarations, expressions statements,  and operators

 + expression consist of a sequenced constant, identifiers and operators that the program evaluate. (the expresion purpose may be to obtaine a result value or produce side effects) a single constant, string literal, or identifier of object or function is in itself an expression.

 + statement is an expression followe by a semicolon, the type and value of the expression are irrelevanta and are deiscarded the next statemente is executed

   - block statements `{ [] }`
   - loop statements
   - selection statements
   - switch statemens
   - unconditional jumps
   - return statements

## comments

```c
// single line comment

/*
 * multi line comment
 */

// you can't nested comments
```

## variables and constants

a variable in C is a name used to refer to some address location in memory ;-), a const variable it is a read only variable 

```c
int a = 42;
const int a_const = 42;
```

## scoping of variables

- global variables (into single file)

```c
int variable_global;

int inc(){
	variable_global++;
}

int main(){
	variable_global = 0;
}
```

- global variables (multiples files)

```c
//int main.c
int variable_global;
int main(){

}
```

```c
extern int variable_global;
int inc(){
	variable_global++;
}
```

- static variables

  + static var only  the code into same file are declared can be access to 
  + static vars into function, only can be acceses into the function and keep the value between execution of function

```c
#include <stdio.h>
int inc(){
	static int counter = 0;
	counter++;
	printf("counter=%d\n",counter);
}
int main(void){
	inc();
	inc();
}
// counter=1
// counter=2
```
## operator precedence and associativity

- (postfix operator) associativity Left to right

```c
[]
()
.
->
++
--
``` 

- unary operator (right to left)

```c
++ -- ! ~ + - * & sizeof _Alignof
```

- cast operator (right to lef)

```c
(type)var
```

- multiplicative operators (left to right)

```c
* / %
```

- additive operator

```c
+ -
```

- shift operator

```c
x << y // each bit value in x is moved y position to left
x >> y // each bit value in x is moved y position to right
```

- relational operator

```c
< <= > >=
```

- equality operator

```c
== !=
```

- bitwise and

```c
&
```
- bitwise exclusive or


```c
^
```

- bitwise or


```c
|
```

- logical and

```c
&&
```

- logical or


```c
||
```

- the conditional/ternary operator ?: 


```c
?:

// example
x<0 ? -1 : 0;
```

- assignaments operator


```c
= += -= *= /= %= &= *= ^= |= <<= >>= 
```

- comma operatyor


```c
,
```

## literal values

```c
// NOT STANDARD
int i = 0b0000000000; // 0b indicate that is binary 
int i = 0B0000000000; // 0b indicate that is binary 

// NOT STANDARD, only historical reasons...
int i = 001;

// STANDARD
int i = 0x01; // 0x indicate that is hexadecimal value
```


## memory addressing operators

- address of `&`

```c
// &x  address of x
int x = 0;
int *ptr = &x; 
```

- indirection operator `*`

```c
// *p the value or function that p points to
```

- subscripting

```c
x[y] // the elemente with index y in the array x
```
- struct or union

```c
x.y
```

- struct or union by a reference

```c
p->y
```




## preprocessor directives

- `#define` is pre-processor directive

This statement is use a lot in embedded programming and is very useful to use with constants, some people referred to as a lambda function

```c
// a constant value
#define CNAME value
#define CNAME "cool-start-with-c"
// a expression 
#define CNAME (expression)
#define CNAME (20 / 4)
// hint never put a semicolon

// likewise use for creation of function-like macros.
#define MAX(x,y) ((x) > (y) ? (x) : (y))
```

-  `#if`, `ifdef`, `ifndef`, `elif`, `else`

these preprocessor directives are used for conditional compilation in the program. In embedded programing are used for debugging and develop libraries that target multiples chips

```c
#ifdef PIC16F1717
#define SPEED 200
#elif defined (__PIC24F__)
#define SPEED 300
#else
#define SPEED 1000
#endif
```

- `#pragma`

this is a C directive that in general purpose is used for machine or operating system specific directives. it providing additional information to the compiler. for instance to configure somer register general purpose.

## datatypes

- basic types

  + standard and extending integer types
  + standard and extending float-point types

- enumerated types

- the type `void`

- derived types

  + pointer types
  + array types
  + structure types
  + union types
  + function types

the types can include or not the object's storage size, if it does the type called `incomplete type` if not `complete type`

```
int complete[5]= {0,1,2,3,4};
extern float incomplete[ ]; // external because size are in another location
```

type scalar or 

### boolean

```c
_Bool     bool(defined in stdbool.h)
// true  1
// false 0
```
also can use macro bool 

### integer

```
unsigned char         0..255           1 byte   
signed char        -128..127  
char 

unsigned int                           2 or 4 bytes
short                                  2 bytes
unsigned short                         2 bytes
long                                   4 bytes
unsigned long                          4 bytes

long long                              8 bytes
unsigned long                          8 bytes
```

specifying size from C99 standard

```c
N={8,16,32,64}
intN_t
uintN_t

int_lestN_t
uint_lestN_t

int_fastN_t
uint_fastN_t

intmax_t
uintmax_t

intptr_t
uintptr_t

```

### floating point

```c
float                            4 bytes
double                           8 bytes
long double                      10 bytes
```

### Enumerated 

```
enum [identifier] { label, label, label };
enum [identifier] { white=1, black=0};
enum running { OFF, ON, SUPPORT_NEED}
```

### the type `void`

the type void specify that no value is available:

- you can use for function which no return 
- you can use for a function paramente list
- you can do a cast (void) expression, explicitly idscards teh value of an expression
- you can use pointer to void `void *`  is like a multipurpose pointer 


### char, wide char and multibyte char

since 1994, C provide type char but also `wchar_t` defined into stddef.h 

```c
#include <stddef.h>

int main(int argc, char *argv[]){
	wchar_t wc = '\x3b1'; // '\x' is scape character in hexadecimal
}
```

since 2011, `C11` improved unicode support with `char16_t`  `char32_t`

wide character vs multibyte, The key difference between multibyte character and wide characters( wchar_t, char16_t or char32_t) is that wide characters are all the same size and multibyte string are more complicated to process thant strings of wide 


Multibyte characters are well for saving text in files, are independent of system architecture while encoding of wide characters is dependant on the given system's byte order: big-endian or little-endian

```c
wchar_t wc = L'\x3B1';
char mbStr[10] = "";
int nBytes = 0;
nBytes = wctomb(mbStr, wc); // wctomb wide character to multi byte ... stuff c
// c16rtomb()

```

universal character names, c supports universal character names as a way to use the extede character set regardless of the implementation's enconding

```c
\uXXXX      // equivalent \U0000XXXX   
\UXXXXXXXX  // 8 char in hex
char alpha = '\u03B1'
```

c provide alternative representation for some punctuation marks that are not available on all keyboard, are named digraph

```c
<:   [
:>   ]
<%   {
%>   }
%:   #
```

```c
int arr<::> = <% 1, 2, ,3 %>
// equivalent
int arr[] = {1, 2, 3}
```

c provide alternative with three-character, are named trigraphs

```
??(    [
??)    ]
??<    {
??>    }
??=    #
??/    \
??!    |
??'    ^
??-    ~
```


### literals

a literal denote a fixed value. it is like a constant of determinated value

```c
int i = 127;
float f = 2.34E5; // 2.34 * 10^5
char c = 'a'
char null_char = '\0'; //'\x0'

char document_path[128] = "\\home\\user\\documents\\this.txt"
char using_uft8
```

### typedef

```c
typedef unsigned char BYTE;

typedef struct Books {
	char title[50];
	char author[50];

} Book;
```

## casting (type conversion)

- conversion of arithmetic types

  + any two unsigned types have diferent rank, converto higher rank
  + each signed integer type has the same rank as corresponding unsigned type
  + `_Bool` < `char` < `short` < `int` < `long` < `long long`,
  + any standear intenger type has a higher rank than an extedned integer type of the same width
  + every enumerated type has the same rank as its corresponding integer type
  + float < double < long double


- explicit pointer conversions

to convert a pointer from one pointer type to another, you must usually use an explicit cast.

```c
float f_var = 1.5F;
long *l_ptr = (long*)&f_var;
double *d_ptr = (double*)l_ptr;
// CAUTION: the platform has sizeof(float) equal sizeof(long)
```

- function pointers

```c
#include <math.h> // declare sqrt function
typedef double(func_t)(double); // define a pointer to func_t which take double and return a double

func_t *pFunc = sqrt; // declare pFunc as pointer to function sqrt
double y = pFunc(2.0);  // a function call througth pointer function

double = (func_t*)abs; // redirect pointer from sqrt to abs function
y = pFunc(2.0);  // a function call througth pointer functiony = pFunc

double = (func_t*)pow // WORKS despite pow takes 2 argumenta and 
y = pFunc(2.0)       // ERROR
```

- pointers to void

are used as multipurpose, pointers to represent the address of any object without regard for its type, malloc return a pointer to void. 


```c
int(*compare)(const void* e1, const void* e2);

void qsort(void *array, size_t n, size_t element_size, int(*compare)(const void*, const void*) );

```

- conversion pointer - integer

you can explicitly convert a pointer to an integer type and viceversa. the result depends off the compiler and should be consistente with the addressing structure of the platform


## arrays

- The declaration of an array should define his type and the number of elements

```c
// FIXED ARRAY
// type array_name[number_of_elements]
char buffer[4*128];
// sizeof(buffer) = 512 * sizeof(char)
int int_array[10];
static int int_array[10];


// NO-FIXED ARRAY
void function_example(int variable_size){
	int int_array[2*n];
	static int other[n];

	struct S { int f[n]; }
}
```

- fixed array 

In C, you can write
```
#define A 8
int arr[A];
// Note: that on C++, both will work.
```

but you can not:
```
const int A = 8;
int arr[A];
// Note: that on C++, both will work.
```


In C, const is a misnomer for read-only. const variables can change their value, e.g. it is perfectly okay to declare

```
const volatile int timer_tick_register; /* A CPU register. */
```

- access to elements into

```c
int array_example[25];
int i = array_example[5];
```

- declaration and initialization

```c
int a[4] = { 1, 2, 3, 4};
int b[] = {1, 2, 3, 4};
int c[] = {1, 2, 3, 4, };

// be careful with, 2 ,3 ,4 is ignored in the most of compilers
int d[1] = {1, 2, 3, 4, };
```

- a c string: is a continuous sequence of characters terminated by '\0', the null character. The length of a string is considered to be the number of characters excluding the terminating null character. There is no string type in C, ergo there are no operators 

string can be of type char , or wide char.

c11 has also introduce a secure version which ensure that string operation do not exceed the bounds of array

```c
#include <string.h>

char str1[30] = "hey"; // string length: 3, array lenght 4
```

- multidimensional arrays

```c
char screen[1920][1080][2];

char c = screen[0][0][1]


int a[2][3][2] = { {0,0}, {0,1}, {1,1} 
                   {1,0}, {1,1}, {1,1},
                   {1,1}, {1,0}, {0,0} };
```


- arrays as arguments of functions

when the name of an array appears as a function argument, the compiler implicitly converts it into a pointer to the array first element. 

when you pass a multidimensional array its a good idea pass length as parameter


- passing array as param

```
int init(int num[20]){
	for(int i=0;i<20;i++){
		num[i] = 0
	}
}

void main(void){
	int x[20];
	init(x);
}
```


When you pass an array to a function, its address is passed to the function as a pointer. So 

```c
void getArraySize(int arr[]);
//is equivalent to
void getArraySize(int* arr);
```

You can safely use sizeof(arr)/sizeof(arr[0]) only within the scope of declaration of arr.
In your case, the scope of declaration of arr is function main.


## addresses, pointers






### pointer to qalified object types

- c pointer declaration (typed pointer)

```c
#include <stdlib.h> // include the macro NULL
#include <stdio.h>  // include the macro NULL
int *ptr = NULL;    // initialization of pointer, not ready to use, need point to
```
- c pointer declaration (untyped pointer)

```c
void *ptr = NULL;
```

note that `*` is the declaration operator not the indirection operator, it means "pointer to"

- pointer variables with authomatic storage duration start with an undefined value, unless you explicit in declaration (all variables defined into any block have automatic storage unless the are defined as static). All other pointer have as initial value null pointer
 

### & address operator

```c
int i = 15;
int *i_ptr = &i; // i_ptr point to i address using `&`
```

### * indirection operator

```c
int i = 42;
int i_ptr = &i;
*i_ptr=0; // replace the i contain
```

### Null Pointer

the null pointer are implicitly converted to other pointer types as necessary for assignment operations or for comparisons,
no cast needed

```c
#include <stdio.h>
FILE *fp = fopen("file.txt","r");
if (fp == NULL) { // if (!fp)

}
```

### pointer to pointer

```c
char c1 = 'A';
char c2 = 'B';
char *ptr = &c1;
char *ptr2;
char **ptr_ptr = &ptr;

// **ptr_ptr = &(&c2); // ERROR 

ptr2 = &c2;

**ptr_ptr = &ptr2

```

if you pass a pointer to a function by reference so that the function can modify its value, then the function¡s paramenter is a pointer to a pointer


### pointer and type qualifiers

```c
int const volatile * restrict ptr;
```

- `const`     the program can not modify it after its definition, note that conts pointer != const variables
- `volatile`  useful in PIC it's a hint for the compiler indicate that may be modified by oter proccesses or events not only by current program, don't apply optimizations
- `restrict`  it's only a way for programmer to inform about an optimizations that compiler can make. because the object it is only accessed using the restrict pointer.


```c
int n = 0;
const int *constPtr; // the const is the int not the pointer, the pointer can change;

constPtr = &n; // convert the address to type const int *
n = *constPtr + 3; // ok
*constPtr *= 3;
```


### pointer to arrays and arrays of pointers

```c
char *array_pointer[3] = {
	"abc",
	"bc",
	"c"
};
```

### pointer to functions

```c
int *notfuncPtr(int,int); // only a prototype for the funcion

int add(int x, int y){
	return x + y;
}

int (*functionPtr)(int, int); // declaration of pointer to a function

functionPtr = add;

int result = (*functionPtr)(1,1); // right
int result = functionPtr(1,1); // right

//
```



## structs, unions, bit fields

- structs

```c
// struct [tag_name] { member_declaration_list };

struct Date { int month, day, year; }

// 


// accesing
Date birthday;

birthday.month = 1;
birthday.day = 25;
birthday.year = 1990;

birthday->month = 2;
birthday->day = 26;
birthday->year = 1980;
```

- unions: the members of a union all share the same location in memory but only one member can contain value at any given time

```c
union Date { char *date, int unix_time };
```


- structs and union combination


```c
struct Demo {
	union {
		struct {long x,y;}
		struct {float x,y;} fl;
		int
	}
} record;

record.x = 0;
record.fl.x = 0.0;
```

- bit fields into structs, union

members of strutures or unions can also be bit-fields, A bit-field is an integer variable that consists of a specified number of bits.

```c
struct Date {
	unsigned int month : 4; // 4 bits => 0..16
	unsigned int day : 5; // 5 bits => 0..32

}
```


## declarations 

A declaration determines the significance and properties of one or more identirfiers. for instance, `_Static_assert` declaration make that the compiler to test whether a constant expression is nonzeo


- declaration of struct, union or enumeration tag

```c
[storage_specifier ] type declarator [, declarator [, ...]]

// storage_specifier: [extern | static | _Thread_local | auto | register ]

// type: [basic type | void | enumerate | structure | union | name of typedef]

// declarator: [function declarator `(` | array declarator `[` | pointer declarator `*`]

```

- declaration that declarar one or more variable or function identifier
- typedef declaration, which declare new name for existing types
- `_Static_asserts` force to compiler to test an assertion



```c
extern volatile short status;
enum { OFF, ON } toggle = ON;
struct color {unsigned r, g, b}
```


## attributes `__attribute__`

__attribute__ is a compiler directive that specifies characteristics on declarations, which allows for more error checking and advanced optimizations.

the attributes provide a source annotations. Enabling to developer a way to request something to the compiler like: 

- static analyser
- name mangling
- code generation

```c
// Return the square of a number
int square(int n) __attribute__((const));

__attribute__((nonnull (1, 2)));

int square(int n) __attribute__((const));

```



## functions 

```c
int name_of_function();
int name_of_function(){

}

// fro outside of file
extern int name_of_function();
```

C allows you to define functions that you can call them with a variable numbers of arguments like printf

```c
int printf(const char *format, ...);
```

- inline functions

```c
inline void swapf(float *p1, float *p2){
	float tmp = *p1;
	*p1 = *p2;
	*p2 = tmp;
}
```

- recursive functions

```c
int recursion(int value){
	if (value <= 0) return 1;
	if (value > 0) return recursion(value-1)*value;
}
```

- functions with variable numbers of arguments


## instruction control flow 

```c
if (speed = LIGHT){

} else {

}


if (speed == LIGHT){

} else if (speed == 0) {

}
```

```c
switch(speed){
	case 0: 
		// do something
		break;
	case 1:
		// do something
		break;
}
```

```c
for(;;){
	break; //terminate the loop
	// infinite loop
}

while(1){
	if (stop){
		break;
	} else {
		continue; // skip the rest of iteration 
	}

}

// yep into microcontroller still is in use
myLabel: int i=0;
goto myLabel;
```

```c
```


## standard input, standard output


