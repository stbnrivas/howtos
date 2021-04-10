# ActiveRecord

"fat model, skiny controller" it is preferred move most business logic to models.



## ActiveRecord out of rails

NOT WORKING YET:

ERROR Could not load the 'sqlite' Active Record adapter. Ensure that the adapter is spelled correctly in config/database.yml and that you've added the necessary adapter gem to your Gemfile.

```ruby
require 'sqlite3'
require 'active_record'

ActiveRecord::Base.establish_connection(
  adapter:  'sqlite',
  database: 'playground.sqlite',
)

class User < ActiveRecord::Base
end
```


## ActiveRecord basic use CRUD

active record is a design pattern for relational database and ActiveRecord is a rails implementation of active record pattern


1. CREATE:

playing with `bin/rails console`
```ruby
u0 = User.new
u0.name = 'John'
u0.surname = 'Doe'
u0.save

u1 = User.new do |u|
	u.name = 'John'
	u.surname = 'Doe'
	u.save
end

u2 = User.new(name: 'Jane', surname: 'Doe')
u2.save


u3 = User.create(name: 'John', surname: 'Wayne')  # return ActiveRecord if saved. Need check errors
u3 = User.create!(name: 'John', surname: 'Wayne') # return ActiveRecord if saved or raise exception

User.create([
	{name: 'John', surname: 'Wayne'},
	{name: 'Clint', surname: 'Eastwood'}
])

u4 = User.create_or_find_by(name: 'django')


```


2. SEARCH

playing with `bin/rails console`
```ruby
u = User.find(1)              # can raise ActiveRecord::RecordNotFound
users = User.find([1,2,3,25]) # can raise ActiveRecord::RecordNotFound
u = User.find_by(name: 'John', surname: 'Wayne')

	def show
	  @user = User.find(session[:user_id])
	rescue ActiveRecord::RecordNotFound
	  @user = User.create
	  session[:user_id] = @user.id
	end


	class SomeController < ApplicationControeller
		rescue_from ActiveRecord::RecordNotFound, with :invalid_id

		private
			def invalid_id
				logger.error "Attemp to access using invalid id: #{params[:id]}"
				redirect_to some_index_url, notice: 'invalid id'
			end
	end


u = User.where(visible: true)
u = User.where(visible: true, surname: 'Wayne')
u = User.where.not.(visible: true)
u = User.where(visible: true).where("created_at < ?", 1.month.ago)
# chaining where clause don't trigger inmediantly the query

u = User.where("surname like ?", params[:surname]+'%') # RIGHT
u = User.where("surname like ?%", params[:surname])    # WRONG

u = User.all.order(name: :desc)
u = User.all.order(name:, created_at: :desc)
u = User.all.order("surname, name DESC")
u = User.where(visible: true).order(:name).limit(100).offset(100*2)

User.all
```

3. getting data from row, columns using count, select, pluck, ids

playing with `bin/rails console`
```ruby
User.all.count
User.all.select(:id, :name).first.id


User.all.map { |p| [p.id, p.name] } # with map the ActiveRecord object is build
# => [ [1, "John"],[2,"Jane"]]
User.all.pluck(:id, :name) # pluck don't build an ActiveRecord it is more efficient
# => [ [1, "John"],[2,"Jane"]]


User.where(active: true).map { |p| p.id } # with map the ActiveRecord object is build
# => [1,2,3,4]
User.where(active: true).ids # ids don't build the ActiveRecord object
# => [1,2,3,4,5,6]
```

named scoped
```ruby
class User < ApplicationRecord
	scope :active, lambda { where(active: true) }
	scope :recent, -> {where("created_at < ?", 1.week.ago)}
	# -> is sintactic sugar for lambda
	scope :search_by_name, lambda { |word|
		where("LOWER(name) LIKE ?","%#{word.downcase}%")
	}

	scope :search_by_surname, -> (word) { where("LOWER(name) LIKE ?","%#{word.downcase}%") }
	scope :visibles, -> { where(active: true) }
	scope :invisibles, -> { where(active: false) }
end

# use like this:
User.active
User.active.where(name: 'John')
User.recent.active.where(name: 'John')

User.search("J")
```

joins
```ruby
class User < ActiveRecord::Base
	has_many :token
end

class Token < ActiveRecord::Base
	belongs_to :user
end

User.joins(:tokens).size
User.joins(:tokens).where(id: 2)   # use joins whtn you don't need to access the association's attributes
 # inner join
User.includes(:tokens).size
User.includes(:tokens).where(id: 2)# use includes whe you do need to access to the association's attributes
 # left outher join
```

group
```ruby
```

group functions
```ruby
Product.average(:price)
Product.maximum(:price)
Product.minimum(:price)
Product.sum(:price)
Product.count(:price)
```



4. UPDATE:

playing with `bin/rails console`
```ruby
u = User.find(1) # 1 is id
u.name = 'Fake'
u.save   # return true if saved or nil otherwise
u.save!  # return true if saved or raise exception otherwise


u.update(name: 'John', surname: 'Wayne')
u.update!(name: 'John', surname: 'Wayne')

User.update_all(state: 'blocked')
User.update_all(state: 'blocked').where(last_activity: 1.year.ago)
```


5. DELETE:

playing with `bin/rails console`
```ruby
u = User.find(1) # 1 is id
u.destroy

User.delete_all
User.delete_all(state: 'blocked').where(last_activity: 1.year.ago)
```


6. writing your own sql

```ruby
u = User.find_by_sql("select name, surname from users where surname like '%wood' ")
```


## Transaction

```ruby
Product.transaction do
  product = Product.where(id: id).lock("LOCK IN SHARE MODE").first
  product.price *= 1.21
  product.save
end
```





## ActiveRecord

- customize the irregular pluralization

```ruby
ActiveSupport::Inflector.inflections do |inflect|
  inflect.irregular 'tax', 'taxes'
end
```

-  change table name

```ruby
class Tax < ApplicationRecord
  self.table_name = "tax"
end
```

- set existing primary key:

```ruby
class LegacyBook
	self.primary_key = "isbn"
end
```


## ActiveRecord equality `==`

two ActiveRecord are considered equals when have the same class and have de same primary key.

Unsaved models may compare as equal even if the y hve differetn attribute data