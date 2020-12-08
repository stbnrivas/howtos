Mongoid: Ruby ODM framework for MongoDB. The philosophy of Mongoid is to provide a familiar API to Ruby developers who have been using Active Record or Data Mapper, while leveraging the power of MongoDB's schemaless and performant document-based design, dynamic queries, and atomic modifier operations



Mongoose: MongoDB object modeling designed to work in an asynchronous environment. Let's face it, writing MongoDB validation, casting and business logic boilerplate is a drag. That's why we wrote Mongoose. Mongoose provides a straight-forward, schema-based solution to modeling your application data and includes built-in type casting, validation, query building, business logic hooks and more, out of the box.










class Person
  include Mongoid::Document
  field :first_name, type: String
  field :middle_name, type: String
  field :last_name, type: String
end

Below is a list of valid types for fields.

    Array
    BigDecimal
    Boolean
    Date
    DateTime
    Float
    Hash
    Integer
    BSON::ObjectId
    BSON::Binary
    Range
    Regexp
    Set
    String
    Symbol
    Time
    TimeWithZone




# mongoid from irb

```bash
source rails-app/.env RACK_ENV=development irb
```

```ruby
require 'mongoid'
Mongoid.load!("path/to/your/mongoid.yml")
```

other way:

```
client = Mongo::Client.new([ '127.0.0.1:27017' ], :database => 'testdb')
```



# mongoid from rails console

```
cd rails_app
bin/rails console
```

https://api.mongodb.com/mongoid/current/


```
User.all


u = User.new({email: "user@domain.com", password: "123456"})

u.save

puts u.id
5f9ffed5f38023032221b818

User.find("5f9ffed5f38023032221b818")

User.find_by({email: "user@domail.com"})
```


