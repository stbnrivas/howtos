# rails auth{orization,entication}








## PART I - AUTHENTICATION WITH DEVISE




https://github.com/heartcombo/devise#the-devise-wiki

It's composed of 10 modules:

- Database Authenticatable: hashes and stores a password in the database to validate the authenticity of a user while signing in. The authentication can be done both through POST requests or HTTP Basic Authentication.

- Omniauthable: adds OmniAuth (https://github.com/omniauth/omniauth) support.

- Confirmable: sends emails with confirmation instructions and verifies whether an account is already confirmed during sign in.

- Recoverable: resets the user password and sends reset instructions.

- Registerable: handles signing up users through a registration process, also allowing them to edit and destroy their account.

- Rememberable: manages generating and clearing a token for remembering the user from a saved cookie.

- Trackable: tracks sign in count, timestamps and IP address.

- Timeoutable: expires sessions that have not been active in a specified period of time.

- Validatable: provides validations of email and password. It's optional and can be customized, so you're able to define your own validations.

- Lockable: locks an account after a specified number of failed sign-in attempts. Can unlock via email or after a specified time period.


### example

https://github.com/imhta/rails_6_devise_example



add gem to our gemfile
```
bundle add devise
```

install devise into our app and follow the instructions
```
bin/rail g devise:install

      create  config/initializers/devise.rb
      create  config/locales/devise.en.yml
===============================================================================

Depending on your application's configuration some manual setup may be required:

  1. Ensure you have defined default url options in your environments files. Here
     is an example of default_url_options appropriate for a development environment
     in config/environments/development.rb:

       config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }

     In production, :host should be set to the actual host of your application.

     * Required for all applications. *

  2. Ensure you have defined root_url to *something* in your config/routes.rb.
     For example:

       root to: "home#index"

     * Not required for API-only Applications *

  3. Ensure you have flash messages in app/views/layouts/application.html.erb.
     For example:

       <p class="notice"><%= notice %></p>
       <p class="alert"><%= alert %></p>

     * Not required for API-only Applications *

  4. You can copy Devise views (for customization) to your app by running:

       rails g devise:views

     * Not required *

```







create a model for user authentication

```
MODEL=user
bin/rails g devise ${MODEL}

      invoke  mongoid
      insert    app/models/user.rb
      insert    app/models/user.rb
       route  devise_for :users

```

copy default views for actions

```
bin/rails g devise:views
```



visit your routes to see what is available:



GET  http://localhost:3000/users/sign_up
POST http://localhost:3000/users
DELETE  http://localhost:3000/users/sign_up

GET  http://localhost:3000/uses/edit

GET  http://localhost:3000/users/sign_in
POST http://localhost:3000/users/sign_in


GET  http://localhost:3000/users/password/new



```
bin/rails routes


                  Prefix Verb   URI Pattern                    Controller#Action
        new_user_session GET    /users/sign_in(.:format)       devise/sessions#new
            user_session POST   /users/sign_in(.:format)       devise/sessions#create
    destroy_user_session DELETE /users/sign_out(.:format)      devise/sessions#destroy
       new_user_password GET    /users/password/new(.:format)  devise/passwords#new
      edit_user_password GET    /users/password/edit(.:format) devise/passwords#edit
           user_password PATCH  /users/password(.:format)      devise/passwords#update
                         PUT    /users/password(.:format)      devise/passwords#update
                         POST   /users/password(.:format)      devise/passwords#create
cancel_user_registration GET    /users/cancel(.:format)        devise/registrations#cancel
   new_user_registration GET    /users/sign_up(.:format)       devise/registrations#new
  edit_user_registration GET    /users/edit(.:format)          devise/registrations#edit
       user_registration PATCH  /users(.:format)               devise/registrations#update
                         PUT    /users(.:format)               devise/registrations#update
                         DELETE /users(.:format)               devise/registrations#destroy
                         POST   /users(.:format)               devise/registrations#create



<% if !user_signed_in? %>
  <li><%=link_to 'login', new_user_session_path %></li>
  <li><%=link_to 'register', new_user_registration_path %></li>
  <li><%=link_to 'forgot password', new_user_password_path%></li>
<% else %>
  <li><%=link_to current_user.email, edit_user_registration_path %></li>
  <li><%=link_to 'logout', destroy_user_session_path, method: :delete%></li>
<% end %>
```


adding `confirmable` to devise model

```
devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable, :confirmable

  ## Confirmable
  field :confirmation_token,   type: String
  field :confirmed_at,         type: Time
  field :confirmation_sent_at, type: Time
  field :unconfirmed_email,    type: String # Only if using reconfirmable

```



```
db.users.find({})

"confirmation_token" : "i5xEBZ3tHrRxorhV9uLw"
```

go to

```
new_user_confirmation GET    /users/confirmation/new(.:format) devise/confirmations#new
       user_confirmation GET    /users/confirmation(.:format)     devise/confirmations#show
                         POST   /users/confirmation(.:format)     devise/confirmations#create
```



http://localhost:3000/users/confirmation?confirmation_token=i5xEBZ3tHrRxorhV9uLw

http://localhost:3000/users/confirmation?confirmation_token=ur7JBni82yAqQ62Kks5q

TODO: add index for confirmation with mongodb...  HOW?







add `is_admin` field into user.rb

```ruby
field :is_admin, type: Boolean
```


select your controller to revoke access if not is an admin

```ruby
class PagesController < ApplicationController
   before_action :authenticate_user!
   before_action :is_admin?, only: [:action1, :action2]
   ...

   private

   def is_admin?
     flash.alert = "Sorry, you don't have permission to this action."
     redirect_to root_path unless current_user.is_admin?
   end
end

```












attributtes customization: probably you need add more attributtes to model and add as params permit like

```ruby
class ApplicationController < ActionController::Base
  protect_from_forgery with :exception

  before_filter :configure_permitted_parameters, if: devise_controller?

  def configure_premitted_parameters
    devise_parameter_sanitiezer.permit(:sign_up, keys: [:name])
    devise_parameter_sanitiezer.permit(:account_update, keys: [:name])
  end
end
```


BUT this is better extract devise behaviour into a module app/controllers/concerns/devise_params_allow_list.rb

```ruby
module DeviseParamsAllowList
  extend ActiveSupport::Concern
  included do
    before_filter :configure_permitted_parameters, if: devise_controller?
  end

  def configure_premitted_parameters
    devise_parameter_sanitiezer.permit(:sign_up, keys: [:name])
    devise_parameter_sanitiezer.permit(:account_update, keys: [:name])
  end
end
```

```ruby
class ApplicationController < ActionController::Base
  protect_from_forgery with :exception
  include DeviseParamsAllowList
end
```






# PART II - Authorization with pundit gem

```
bundle add pundit
```

add to application controller:

```
class ApplicationController < ActionController::Base
  #...
  include pundit
end
```

```
bin/rails g pundit:install


bin/rails g pundit:policy ${POLICY_NAME}
```






# PART II - Authorization with petergate gem


pre-requirements:

devise... or methods `user_signed_in?`, `current_user`, `after_sign_in_path_for(current_user)`, `authenticate_user!`




```
bin/rails g petergate:install
bin/rails migrate
```



