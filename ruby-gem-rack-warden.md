https://www.youtube.com/watch?v=QBJ3G40fxHg



```ruby
BCrypt::Password.create("123")
```

```ruby



# warden strategies

Warden::strategies.add(:password) do
  # method available into strategies
  # succes!  - log a user or cause (causes halt!)
  # fail!    - sets the strategy to fail (causes a halt!)
  # halt!    - make this one teh last strategy instruction proccessed
  #redirect! - redirects to another url (causes a halt!)
  # custom!  - accepts a custom rack array (causes a halt!)
  # pass     - ignore this strategy (default)
  def valid?
    params["email"] && params["password"]
  end

  def authenticate!
    user = USERS.find do |user|
      user[:email] == params["email"] && user[:password] == params["password"]
    end
    if user.nil?
      fail!("invalid authentication")
    else
      success!(user)
    end
  end

end


# howto use into controllers:
#
# env["warden"].authenticate     # authenticate with the default strategy
# env["warden"].authenticate(:password)   # authenticate with the password strategy
# env["warden"].authenticate(:password, :api_token)    # authenticate with the password strategy if fails try api_token
#


# warden setup

use Rack::Session::Cookie, secret: "warden"

use Warden::Manager do |manager|
  manager.default_strategies :password
  manager.failure_app = FailureApp.new
end

run MyApp.new

class FailureApp
  def call(env)
    status = 401
    headers = { "content-type" => "application/json"}
    body = ["something was wrong"]
    [status, headers, body]
  end
end




def authenticate!
	user = USERS.find{|user| user[:email] == params["email"]}
	return fail!("Invalid authentication") if user.nil?

	if BCrypt::Password.new(user[:password]).is_password?(params["password"])
		success!(user)
	else
		fail!("Invalid authentication")
	end
end

```



warden scope to get some like roles

```ruby
env["warden"].authenticate(:api_token, scope: :customer) # auth with api_token strategy in customer scope

env["warden"].authenticated? # without scope default is used

env["warden"].authenticated?(:customer) # check customer scope

env["warden"].user(:customer) # fetch the customer

env["warden"].logout
env["warden"].logout(:default)
env["warden"].logout(:customer)


use Warden::Manager do |config|
	config.default_scope = :customer
	config.scope_defaults(:customer, strategies: [:password])
	config.scope_defaults(:editor, store: false, strategies: [:editor, :account_owner])
end
```



callback

```ruby
Warden::Manager.after_set_user do |user, warden, opts|
end
Warden::Manager.after_set_user except: :fetch
Warden::Manager.after_set_user only: :authentication
Warden::Manager.after_set_user only: :fetch
Warden::Manager.after_set_user scope: :admin

Warden::Manager.after_authentication

Warden::Manager.after_fetch

Warden::Manager.after_failed_fetch
Warden::Manager.on_request
Warden::Manager.before_failure
Warden::Manager.before_logout do |user, warden, opts| 
end
Warden::Manager.before_logout scope: :admin do |user, warden, opts|
end




trigger actions
env["warden"].user
env["warden"].authenticate
env["warden"].set_user(user)
```