# module Enumerable

```ruby
x = [1,2,3,4,5,6,7.8]
x.map {|x| x*x} []
x.max
x.min


%w[ant bear cat].all? { |word| word.length >= 3 } #=> true
%w[ant bear cat].all?(/t/)                        #=> false


%w[ant bear cat].any? { |word| word.length >= 3 }

x.any?(&:odd?)


x.detect{|i| i>4} # first elemente that success condition

x.reduce(&:*)

x.select(&:odd?)
x.take_while{|x| x < 4}

x.group_by{|e| e % 3} # [1=>[3,6,9],2=>[1,4,7],3=>[2,5,8]]
x.each_slice(3){|slice| p slice}  
# [1,2,3]
# [4,5,6]
# [7,8,9]

x.partition(&:odd?)


```


to reach all this methods only need implements each and add the module 
or


