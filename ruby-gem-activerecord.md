# ActiveRecord

active record is a design pattern for relational database and ActiveRecord is a rails implementation of active record pattern

```ruby
user = User.new
user.first_name = "John"
user.save

user.delete
```


1. playing with `bin/rails console` creation

```ruby
u = User.new
u.name = 'John'
u.surname = 'Doe'
u.save


u2 = User.new(name: 'Jane', surname: 'Doe')
u2.save


u3 = User.create(name: 'John', surname: 'Wayne')


u4 = User.create_or_find_by(name: 'django')

```


2. playing with `bin/rails console` creation
```ruby
u = User.find(1) # 1 is id

u = User.find_by(name: 'John', surname: 'Wayne')

User.all
```


3. playing with `bin/rails console` to update
```ruby
u = User.find(1) # 1 is id
u.name = 'Fake'
u.save


u.update(name: 'John', surname: 'Wayne')


User.update_all(state: 'blocked')
```


4. playing with `bin/rails console` to delete
```ruby
u = User.find(1) # 1 is id
u.destroy
```


# ActiveRelation

is object-oriented interpretation of relational algebra, simplifies the generation of complex database queries and allow that queries are chainable


```ruby
users = User.where(:first_name => "John")
users = users.order("last_name ASC").limit(5)
```
