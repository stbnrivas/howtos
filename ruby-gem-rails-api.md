# ruby on rails --api

by default rails is an overkill for microservices because was proposed --api

- no cookies
- no middleware into web browser
- no assets
- no views
- no active storage
- no action text
- no action mailer
- no ...


```bash
rails new api -T --api
```


add gem 'rspec-rails'
add gem 'factory_bot_rails'


```bash
bin/rails generate rspec:install
rspec

# without migration
bin/rails g model Article --skip-migration

# class Article < ActiveRecord::Base
#   self.table_name = "not_cool_table_name"
# end

# with migration
bin/rails generate model Article title:string content:text slug:string
bin/rails db:migrate


bin/rails destroy model Article
```

to test dabase connection, right now you can run rails console

```bash
bin/rails console
```



```bash
rspec spec/models/article_spec.rb
```


gem 'active_model_serializers'
active_model_serializer because appears created_at and updated_at when
```ruby
articles = Articles.all
render json: articles
```

create articles_controller.rb
spec/articles_controller_spec.rb


```bash
rspec spec/models/article_spec.rb
rails generate serializer article title content slug
```

create new initializer

config/initializer/active_model_serializers.rb











```ruby
class Api::V1::UsersController < Api::V1::BaseController
    def index
      # ...
    end

    def create
      # ...
    end

    def show
      # ...
    end
end
```

```ruby
class Api::V2::UsersController < Api::V1::UsersController
    def index
      # changes to the index method ...
    end

    # create and show methods have the same behaviour as in V1
end
```


routes.rb

```ruby
  scope module: 'web' do
    namespace :admins do
      resources :users
    end
  end

  scope module: 'api' do
    namespace :v1 do
      resources :users
    end
  end
```

use gem 'active_model_serializers' instead of rabl or jbuilder see below example

```ruby
# app/serializers/api/v1/task_serializer.rb
class Api::V1::TaskSerializer < ActiveModel::Serializer
  attributes :id, :subject
  attribute :status, if: :public?
  belongs_to :creator, serializer: Api::V1::UserSerializer
  belongs_to :assignee, serializer: Api::V1::UserSerializer
  delegate :accepted?, to: :object
end

# app/serializers/api/v1/user_serializer.rb
class Api::V1::UserSerializer < ActiveModel::Serializer
  attributes :id, :name
end

# app/controller/api/v1/tasks_controller.rb
class Api::V1::TasksController < Api::V1::BaseController
  def index
    tasks = Task.all
    render json: tasks, each_serializer: Api::V1::TaskSerializer, root: false
  end
end
```


## Errors handling

Dealing with errors is rarely an easy thing in web applications. The main challenge here is to provide a unified API errors format. The idea is simply based on an hierarchy of exceptions. There is a base error class called “ApplicationError” and all errors are inherited from it.





# ruby on rail --api (other example)


# api with rails




rails new api --api

rails g scaffold


```ruby

render json: @user.to_json(only: [:id, :username])

@user = User.new(user_param)

def user_params
end


#versioning de api

namespace :api do
	namespace :v1 do
		resources
	end
end

gem jbuilder

view /api/v1/user/show/
	json.id @user.id


namespace :api, {format: json }  do
	namespace :v1 do
		resources
	end
end

jsoni.data do

  json.user do
     json.id @user.id
      end
  end
```

doorkeeper only for API OAuth 2 provider as rails engine



