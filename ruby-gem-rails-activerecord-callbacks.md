## ActiveRecord Callback

[https://guides.rubyonrails.org/active_record_callbacks.html](https://guides.rubyonrails.org/active_record_callbacks.html)


```
|         CREATE        |         UPDATE         |        DESTROY         |
|-----------------------|------------------------|------------------------|
|   before_validation   |    before_validation   |                        |
===========================================================================
|                               VALIDATION                                |
===========================================================================
|    after_validation   |     after_validation   |                        |
|      before_save      |       before_save      |                        |
|      before_create    |       before_update    |     before_destroy     |
===========================================================================
|                           DATABASE CONNECTION                           |
===========================================================================
|      after_create     |       after_update     |     after_destroy      |
|      after_save       |       after_save       |                        |
|      after_commit     |       after_commit     |     after_commit       |
```


1. basic usage
```ruby
class Customer < ApplicationRecord
  before_validation :format_phone
  before_save :geocode_from_address
  after_commit :email_confirmation

  private # or protected

  def format_phone
  end

  def geocode_from_address
  end

  def email_confirmation
  end
end
```


2. conditional callback
```ruby
class Customer < ApplicationRecord
  after_save   :email_to_admin, if: is_admin?
  after_commit :email_to_admin, unless: !is_admin?

  def is_admin?
  end

  private # or protected

  def email_to_admin
  end
end
```

```ruby
class Customer < ApplicationRecord
  after_save   :email_to_admin, if: Proc.new { |c| c.email.end_with? 'mydomain.com' }

  def is_admin?
  end

  private # or protected

  def email_to_admin
  end
end
```

3. skipping callback

the way to skip the callback is constructing the sql

```ruby
c = Customer.new
# ...

c.update_colum(:name, new_name)                        # trigger callback
c.update_columns(name: new_name, surname: new_surname) # trigger callback

c.delete # DON'T TRIGGER CALLBACK

```

```ruby
Product.where("update_at < ?", 5.years.ago).update_all(active: false)
Product.where("active = ?", false).delete_all
```


or you can build the logic to skip

```ruby
class Customer < ApplicationRecord
  after_commit :email_to_admin, unless: skip_email?

end

c = Customer.new
c.skip_email = true
c.save
```