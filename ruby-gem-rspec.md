# rspec

think about user stories, describe a single step based in

- Given
- When
- Then

What do you want to test
- happy path
- unhappy path
- edge cases
- any bug that gets fixed

What you don't want to test

- basic ruby
- basic ruby on rails
- third party APIs (unless they are not trustable)
- behaviors being tested already

Advices

- a bad, partial or broken test can be worse than none
- keep test fast and this way you will run it more often
- run test often
- avoid fragile test

mock the views is interesting

- you only have to thest the parts that need to work
-

## installation

```bash
gem install rspec
```

## using rspec into irb

```bash
irb
```

```ruby
require 'rspec/core'
require 'rspec/expectations'
include RSpec::Matchers

expect(1).to eq(1)
```

## configuration

	~/.rspec		Global
	./.rspec		Into project folder probably added to repo
	./.rspec-local		Local or personal customization, not add to control version



|	by default				|		other option |
|-------------------|------------------------------------|
|	--no-color 				|		--color					|
|	--format progress	|		--format documentation			|
|	--no-profile			|		--profile			|
|	--no-fail-fast		|		--fail-fast			|
|	--order defined		|		--order random			|


## file structure in rspec

- all file with test must be `_spec.rb` as suffix
- the `_spec.rb` file must require staff to spec
- you can create folder like `models` `integration`


## block organization in rspec

Usually rspec hierarchy is

- spec file `some_spec.rb`
	+ example group using `describe`
		- nested group using nested `describe` | `context`
			+ particular spec using `it`
				- expectations using `expect().to()`



```ruby
describe "a grouping of spec" do

end
```

describe blocks can be nested

```ruby
describe "a general grouping of spec" do
	describe "a less general grouping of spec" do

	end
end
```

sometime can use `context`  which is an alias of `describe`

```ruby
describe "a general grouping of spec" do
	context "a less general grouping of spec" do

	end
end
```

by convention

```ruby
describe ".instance_method" do
end

describe "#class_method" do
end
```


```ruby
it "particular case of specification" do

end
```



+ happy way
+ edge


## pending and skipping

- `skip` used to indicate that an example should be skipped and not executed. use when no implementation provided
- `pending` used  to indicate that an example is disabled pending some action.

```ruby
it "amazing test block" do
	pending
end

it "amazing test block" do
	pending("providing a reason: debugging problem")
end
# or
it "amazing test block"
```

```ruby
xdescribe "amazing test context" do

end

describe "amazing test context" do
	skip
end

describe "amazing test context" do
	skip("providing a reason: debugging problem")
end

xit "amazing test block" do
end

it "amazing test block" do
	skip
end
```


## expectation sintax

expect $argument_to_test .to $argument_expected

```ruby
expect( ).to()
expect( ).not_to()
```
In general, use one expectation per example because with more you will only see the first failure, the next expectation never will be executed. and all test will be more parallelizable

## matchers

- equivalence matchers

```ruby
expect(x).to eq(1)
expect(x).to be == 1
expect(x).to eql(1)
expect(x).to equal(1)

expect(x).not_to eq(1)
expect(x).not_to be == 1
expect(x).not_to eql(1)
expect(x).not_to equal(1)
```

- truth matchers

```ruby
expect(1==1).to be true
expect(1==1).to be(true) # prefered because nil can be consider false in evaluation

expect(1!=1).to be false
expect(1!=1).to be(false) # prefered because nil can be consider false in evaluation

expect(1==1).to be_truthy
expect(1==1).to be_falsey

expect(nil).to be_nil
expect(nil).to be nil # in this it doesn't matter
```

- numeric comparison matchers

```ruby
expect(100).to eq(100)
expect(100).to be ==100
expect(100).to be >99
expect(100).to be <101
expect(100).to be >=101
expect(100).to be <=101

expect(5).to be_between(3,5).inclusive
expect(5).not_to be_between(3,5).exclusive
expect(100).to be_within(5).of(105)
expect(1..10).to cover(3)

```

- collection matchers

```ruby
expect([1,2,3]).to include(2)
expect([1,2,3]).to include(2,3)

expect([1,2,3]).to start_with(1)
expect([1,2,3]).not_to end_with(4)

expect([1,2,3]).to match_array([3,2,1])
expect([1,2,3]).not_to match_array([1,2])

expect([1,2,3]).to contain_exactly(2,1,3)
```

```ruby
expect("hello world").to include('world')
expect("hello world").to include('hello','world')

expect("hello world").to start_with('hell')
expect("hello world").to end_with('ld')
```

```ruby
cities = { granada: true, malaga: true }
expect(cities).to include(:granada)
expect(cities).to include(:granada,:malaga)
```

- regular expression matcher

```ruby
expect('Hello world').to match(/^H.+d$/)
expect('123').to match(/\d{3}/)
```

- object type matcher
```ruby
bob = Object.new
expect(bob).to be_instance_of(Object) # more restrict
expect(bob).to be_an_instance_of(Object)
expect(bob).to be_an_instance_of(Object)

expect(bob).to be_kind_of(Object)
expect(bob).to be_a_kind_of(Object)

expect(bob).to be_a(Customer)
expect([1,2,3]).to be_an(Array)

```
- respond to matcher
```ruby
some = Array.new
expect(some).to respond_to(:at)
```

- attributte matcher
```ruby
some = MyClass.new
expect(some).to have_attributtes({first_name: 'john'})
expect(some).to have_attributtes({first_name: 'john',second_name: 'doe'})
```


- satisfy matcher
```ruby
# satisfy don't take argument, take a block
expect(5).to satisfy {|v| v < 9 && v.odd?}
expect(some).to satisfy do |e|
	element.valid? && element.enabled?
end
```

- predicate matchers

```ruby
expect(value).to be_nil
expect(value).to be_odd
expect(value).to be_even
expect(value).to be_zero
expect(value).to be_nonzero
expect(value).to be_integer
expect(value).to be_empty
```

- observation matchers

```ruby

```

## running spec customization

```bash
rspec
# specific file
respec spec/models/some_model_spec.rb
# specific test which start on line 7
respec spec/models/some_model_spec.rb:7
# specific configuration
rspec --format progress
rspec --format documentation
rspec --order random
rspec --profile
rspec --fail-fast
```

## running spec order

```bash
rspec --order define
d```

## fixtures and factories

- fixtures are writes in yaml and stores in spec/fixtures folder
you can use gems like faker and do loop

```yaml
me:
  name: 'john doe'
<% 5.times do |n| %>
  person_<%=n%>:
    name: <%= Faker::Name.name %>
<% end %>
```

- factories as factory_bot is stored spec/factories, don't automatically loaded
