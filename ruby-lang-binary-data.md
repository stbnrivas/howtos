# ruby pack, unpack

C programming language allows developers to directly access the memory where variables are stored. Ruby does not allow that. There are times while working in Ruby when you need to access the underlying bits and bytes. Ruby provides two methods pack and unpack for that.


```ruby

'A'.unpack('b*')
#=> ["10000010"]

'A'.unpack('B*')
#=> ["01000001"]

############

C             | Integer | 8-bit unsigned (unsigned char)

'A'.unpack('C*')
#=> [65]

[0x65].pack('C*')
#=> "e"

```





## MSB vs LSB, Most significant bit vs Least significant bit


