# bundler cheatsheet

```bash
bundle init
bundle check

bundle install $GEM_NAME

bundle outdated

bundle update
bundle update --source $GEM_NAME

bundle show sinatra
# /path/to/project-folder/vendor/bundle/ruby/2.2.0/gems/sinatra-2.0.0
```


## Deployment the Bundler way that install into vendor folder

```bash
bundle install --deployment
bundle install --path vendor/bundle

bundle show gem_name
```

## gem creation with bundle

```bash
bundle gem 
```

# Gemfile example

```ruby
# frozen_string_literal: true
source "https://rubygems.org"

git_source(:github) {|repo_name| "https://github.com/#{repo_name}" }

gem "gem_name"
gem "gem_name", "=3.48.0"
gem "gem_name", "~> 3.0"	

group :test do
	gem 'hello'
end

group :development do
	gem 'hello'
end
```

# install your gems into verdor folder

```bash
bundle install --path vendor/bundle
```

