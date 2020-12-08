https://semaphoreci.com/blog/2014/01/14/rails-testing-antipatterns-fixtures-and-factories.html


# loading seed into rspec




```
# rails_helper.rb
RSpec.configure do |config|
  config.before :suite do
    Rails.application.load_seed
  end
end
```