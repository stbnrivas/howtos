

## validations on active record

```ruby
class Person < ApplicationRecord
  validates :name, presence: true
end


Person.new().valid?
Person.new().invalid?

Person.new().new_record?
# => true
Person.new().save.new_record?
# => false
```

- validates_acceptance_of
- validates_associated
- validates_confirmation_of
- validates_exclusion_of
- validates_format_of
- validates_inclusion_of
- validates_length_of
- validates_numericality_of
- validates_presence_of
- validates_uniqueness_of
- validates_each



validation standard options:

- `:allow_nil`
- `:allow_blank`
- `:on (:save, :create, :update)`
- `:if, :unless`
- `:message`




- `validates_acceptance_of` must be accepted, cool for checkbox got checked
```ruby
validates_acceptance_of :terms_of_service
validates_acceptance_of :terms_of_service, :accept => 'yes'
```

- `validates_associated` associated object(s) must all be valid
```ruby
```

- `validates_confirmation_of` must be confirmed by writing two times, cool for password confirmation using virtual attribute like `email` `email_confirmation`.
```ruby
validates_confirmation_of :email
```

- `validates_exclusion_of`
```ruby
```

- `validates_format_of` must match a regular expression, cool for email, phone number, zip codes
```ruby
validates_format_of :zipcode, with: /\d{5}/
```

- `validates_inclusion_of` must be in alist of choices (array or range)
```ruby
validates_inclusion_of :status, in: [:active, :unconfirmed, :blocked]
validates_inclusion_of :price, in: [100, 500]

# in or withing are same
```

- `validates_length_of`
```ruby
validates_length_of :name, within: 3..40
```
- `validates_numericality_of`
```ruby
validates_numericality_of :price, equal_to: 0
validates_numericality_of :price, greater_than: 0
validates_numericality_of :price, greater_than_or_equal_to: 0
validates_numericality_of :price, less_than: 0
validates_numericality_of :price, less_than_or_equal_to: 0
```

- `validates_presence_of` must not be blank (nil, false, "", " ", [], {})
```ruby
validates_presence_of :name
validates_presence_of :card_number, :if => :paid_with_card?

validates :name, :surname, presence: true
```

- `validates_uniqueness_of` must not exist in the database
```ruby
validates_uniqueness_of :nif

validates_uniqueness_of :title, case_sensitive: false
validates_uniqueness_of :book_title, :scope => :editorial, :message => "book title should be once per editorial"
```

- validates_each
```ruby
```




### validates the multipurpose validation on same attribute

```ruby
class Person < ApplicationRecord
  validates_presence_of :email
  validates_length_of :email, :maximum => 50
  validates_uniqueness_of :email
  validates_format_of :email
  validates_confirmation_of :email
end

class Person < ApplicationRecord
  validates :name, :presence => true,
                   :length => { maximum: 50 },
                   :uniqueness => true,
                   :format => { with: EMAIL_REGEX },
                   :confirmation => true
end
```


### custom validation

```ruby
class Person < ApplicationRecord
	validate :custom_method

	private
	def custom_method
		if true
			errors.add(:attribute, "message")
		end
		if true
			errors.add(:attribute, "other message")
		end
	end
end
```
