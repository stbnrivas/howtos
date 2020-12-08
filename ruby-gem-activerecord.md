# ActiveRecord

active record is a design pattern for relational database and ActiveRecord is a rails implementation of active record pattern

```ruby
user = User.new
user.first_name = "John"
user.save

user.delete
```

# ActiveRelation

is object-oriented interpretation of relational algebra, simplifies the generation of complex database queries and allow that queries are chainable


```ruby
users = User.where(:first_name => "John")
users = users.order("last_name ASC").limit(5)
```