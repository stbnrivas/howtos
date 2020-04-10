# python cheatsheet

## python const

```python
GRAVITY = 9.8
PI = 3.14
```

## literals

```python
#Binary Literals
a = 0b1010 
#Decimal Literal 
b = 100    
#Octal Literal
c = 0o310  
#Hexadecimal Literal
d = 0x12c  

#Float Literal
float_1 = 10.5 
float_2 = 1.5e2

#Complex Literal 
x = 3.14j
```

## python data types

```python
type(123)
type(123.456)
type(6+4j)
type("hello")
type({})
type([1,2,3,4])
type((1,2,3,4))
```


Boolean
```python
x=True
y=False
```

String
```python
s1 = 'hello'
s2 = "world"

print(s1[0])
print(s1[0:1])
print(s1[1:])
print(s1[:2])

s3 = str(3+5j)

n1 = 'Hello'
n2 = 'world!!'
print("% s  % s."%(n1, n2)) 
```

interpolation
```python
s1 = " hello {}"
s2 = s1.format("world")
```


Complex number
```python

```


List: are mutable
```python
l1=[1,2,3,4]
l2=["john",2,{}]

print(l[-1])
print(l[1:])
print(l[:2])
```


Tuple: the tuple is immutable
```python
example_tuple = (1,2,3,4)
print example_tuple[0]
print len(example_tuple)
```


Set
```python
s = {"hello", "world"}
s.add("howdy")
```


Dictionary
```python
{1:"one", 2:"two", 3:"three"}
```

## mutable and immutable objects





## conditional operators


```python
if b > a:
  print("b is greater than a")

# shorthand
if a > b: print("a is greater than b") 


if b > a:
  print("b is greater than a")
elif a == b:
  print("a and b are equal")
else:
  print("a is greater than b")
# shorthand
print("A") if a > b else print("B")



if False
	pass

```



python don't have switch statement

## operators logic


```python
if True or False: print("ok")

if False and False: pring("not ok")
```


## functions


```python
def add(x,y):
	return x+y

print add(4,2)
```

```python
def add(x,y=0):
	return x+y

print add(x)
```


## lambda functions

```python
def add(x, y):
	return x+y
print(add(5,7))

add2 = lambda x, y: x+y
print(add2(5,7))
print((lambda x, y: x+y)(5,7))
```


## loop statement

```python
t=(2,'a',2+7j)
i=0
while i<len(t):
	print(t[i])
	i=i+1
```


```python
t=(2,'a',2+7j)
for x in t:
	print(x)


t2=(0,1,2,3,4,5,10,11,12)
t2[0:1]
t2[:3]
t2[3:]
```



## OOP in python


- show methods available

```python
dir({})

# ['__class__', '__cmp__', '__contains__', '__delattr__', '__delitem__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'clear', 'copy', 'fromkeys', 'get', 'has_key', 'items', 'iteritems', 'iterkeys', 'itervalues', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values', 'viewitems', 'viewkeys', 'viewvalues']

```

- a class


```python
class Person:
	pass
```


```python
class Person:
	def __init__(self, name):
		self.name = name

	def __str__(self):
		# like toString
		return f"Person: {self.name}"

	def __repr__(self):
		# unambiguous representation
		return f"<Person {self.name}>"

```

```python
class Person:
	salary=0.0
	hours_worked=0

	def __init__(self):
		self.salary = 1

	def workOneDay(self):
		self.hours_worked = self.hours_worked + 8

	def workOneDay(self,amount):
		self.hours_worked = self.hours_worked + amount

```

- inheritance

```python
class Base:
	def __init__():

class Son(Base):
	def __init__(self)
		super().__init__()
	

```


