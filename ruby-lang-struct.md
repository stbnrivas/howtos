struct outside of a method


```ruby
SelectOption = Struct.new(:display, :value) do
  def to_ary
    [display, value]
  end
end

option_struct = SelectOption.new("Canada (CAD)", :cad)

opction_struct.display
opction_struct.value
```

struct inside of a method

```ruby
def a_cool_method
    Struct.new('StructOutputReplyRaw', :status)
    output_reply_raw = Struct::StructOutputReplyRaw.new(200)
end
```