# DRY with F5 to update

## for rack apps

+ step 1: add to your gemfile, and install

```ruby
group :development do  
  gem 'rack-livereload', '~>0.3.17'
  gem 'guard', '~> 2.8'
  gem 'guard-livereload', require: false # 0.3.17
end
```

```bash
bundle install
```

+ step 2: create a 'Guard' file

```bash
# check if works
bundle exec guard --help
# Guard file creation
bundle exec guard init livereload
```


+ step 3: customization of

```ruby
# More info at https://github.com/guard/guard#readme
guard 'livereload' do
  watch(%r{app.rb})
  watch(%r{views/.+\.(erb)})
  watch(%r{helpers/.+\.rb})
  watch(%r{public/.+\.(css|js|html)})
  #watch(%r{config/locales/.+\.yml})
end
```

+ stet 4: set config into confi.ru

```ruby
require 'rack'
require 'rack-livereload'

use Rack::LiveReload
```

+ step 5: enable the guard to start monitor the changes

```bash
bundle exec guard
```

+ step 5: install plugin into browser

it can be 

+ LiveReload by Todd Wolfson (firefox)
+ LiveReload Offered by: livereload.com (chrome)



## for rails apps 

TODO: