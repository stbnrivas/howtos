# ruby binary data packing and unpacking 

in general work with binary is pain in the ass that's where Array#pack and Array#unpack method make your life easier... allowing work with text and converting after



- string to ASCII 

```
str = "abcd"
=> "abcd"
irb(main):002:0> str.unpack("c*")
=> [97, 98, 99, 100]
```

the param `"c*"` is convert to an integer value there are more differents conversions

   + `c` is for char
   + `*` is for repeat previous conversion


```
[97, 98, 99, 100].pack("c*")
=> "abcd"
```


- string to HEX

```
str = "abcd"
=> "abcd"
irb(main):002:0> str.unpack("H*")
=> ["61626364"]
```

   + `H` is for hexadecimal
   + `*` is for repeat previous conversion

```
["61626364"].pack("H*")
=> "abcd"
```



- string to base64


```
"abc".unpack("m")
=> ["i\xB7"]


["i\xB7"].pack("m")
=> "abc=\n"
```





https://ruby-doc.org/core-2.6.5/Array.html#method-i-pack



Integer       | Array   |
Directive     | Element | Meaning
----------------------------------------------------------------------------
C             | Integer | 8-bit unsigned (unsigned char)
S             | Integer | 16-bit unsigned, native endian (uint16_t)
L             | Integer | 32-bit unsigned, native endian (uint32_t)
Q             | Integer | 64-bit unsigned, native endian (uint64_t)
J             | Integer | pointer width unsigned, native endian (uintptr_t)
              |         | (J is available since Ruby 2.3.)
              |         |
c             | Integer | 8-bit signed (signed char)
s             | Integer | 16-bit signed, native endian (int16_t)
l             | Integer | 32-bit signed, native endian (int32_t)
q             | Integer | 64-bit signed, native endian (int64_t)
j             | Integer | pointer width signed, native endian (intptr_t)
              |         | (j is available since Ruby 2.3.)
              |         |
S_ S!         | Integer | unsigned short, native endian
I I_ I!       | Integer | unsigned int, native endian
L_ L!         | Integer | unsigned long, native endian
Q_ Q!         | Integer | unsigned long long, native endian (ArgumentError
              |         | if the platform has no long long type.)
              |         | (Q_ and Q! is available since Ruby 2.1.)
J!            | Integer | uintptr_t, native endian (same with J)
              |         | (J! is available since Ruby 2.3.)
              |         |
s_ s!         | Integer | signed short, native endian
i i_ i!       | Integer | signed int, native endian
l_ l!         | Integer | signed long, native endian
q_ q!         | Integer | signed long long, native endian (ArgumentError
              |         | if the platform has no long long type.)
              |         | (q_ and q! is available since Ruby 2.1.)
j!            | Integer | intptr_t, native endian (same with j)
              |         | (j! is available since Ruby 2.3.)
              |         |
S> s> S!> s!> | Integer | same as the directives without ">" except
L> l> L!> l!> |         | big endian
I!> i!>       |         | (available since Ruby 1.9.3)
Q> q> Q!> q!> |         | "S>" is same as "n"
J> j> J!> j!> |         | "L>" is same as "N"
              |         |
S< s< S!< s!< | Integer | same as the directives without "<" except
L< l< L!< l!< |         | little endian
I!< i!<       |         | (available since Ruby 1.9.3)
Q< q< Q!< q!< |         | "S<" is same as "v"
J< j< J!< j!< |         | "L<" is same as "V"
              |         |
n             | Integer | 16-bit unsigned, network (big-endian) byte order
N             | Integer | 32-bit unsigned, network (big-endian) byte order
v             | Integer | 16-bit unsigned, VAX (little-endian) byte order
V             | Integer | 32-bit unsigned, VAX (little-endian) byte order
              |         |
U             | Integer | UTF-8 character
w             | Integer | BER-compressed integer

Float        | Array   |
Directive    | Element | Meaning
---------------------------------------------------------------------------
D d          | Float   | double-precision, native format
F f          | Float   | single-precision, native format
E            | Float   | double-precision, little-endian byte order
e            | Float   | single-precision, little-endian byte order
G            | Float   | double-precision, network (big-endian) byte order
g            | Float   | single-precision, network (big-endian) byte order

String       | Array   |
Directive    | Element | Meaning
---------------------------------------------------------------------------
A            | String  | arbitrary binary string (space padded, count is width)
a            | String  | arbitrary binary string (null padded, count is width)
Z            | String  | same as ``a'', except that null is added with *
B            | String  | bit string (MSB first)
b            | String  | bit string (LSB first)
H            | String  | hex string (high nibble first)
h            | String  | hex string (low nibble first)
u            | String  | UU-encoded string
M            | String  | quoted printable, MIME encoding (see also RFC2045)
             |         | (text mode but input must use LF and output LF)
m            | String  | base64 encoded string (see RFC 2045, count is width)
             |         | (if count is 0, no line feed are added, see RFC 4648)
P            | String  | pointer to a structure (fixed-length string)
p            | String  | pointer to a null-terminated string

Misc.        | Array   |
Directive    | Element | Meaning
---------------------------------------------------------------------------
@            | ---     | moves to absolute position
X            | ---     | back up a byte
x            | ---     | null byte