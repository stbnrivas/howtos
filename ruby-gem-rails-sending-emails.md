# sending emails into rails

## configuration

same configuration for development,test,production, then use config/environment.rb

```ruby

```


different configuration for every env use config/environments/{development,test,production}.rb

```ruby
Rails.application.configure do
  config.action_mailer.delivery_method = :smtp # :sendmail, :test

  config.action_mailer.smtp_settings = {
  	address:              "smtp.gmail.com",
  	port:                 587,
  	domain:               "domain.example.net",
  	authentication:       "plain",
  	user_name:            "john.doe",
  	password:             "secret",
  	enable_starttls_auto: true

  }
end
```


```bash
bin/rails generate Order received shipped

#   create  app/mailers/order_mailer.rb
#   invoke  erb
#   create    app/views/order_mailer
#   create    app/views/order_mailer/received.text.erb
#   create    app/views/order_mailer/received.html.erb
#   create    app/views/order_mailer/shipped.text.erb
#   create    app/views/order_mailer/shipped.html.erb
#   invoke  test_unit
#   create    test/mailers/order_mailer_test.rb
#   create    test/mailers/previews/order_mailer_preview.rb
```


```ruby
class OrderMailer < ApplicationMailer
  default from: 'Sam Ruby <depot@example.com>'
  # Subject can be set in your I18n file at config/locales/en.yml
  # with the following lookup:
  #
  #   en.order_mailer.received.subject
  #
  def received
    @greeting = "Hi"

    mail to: "to@example.org"
  end

  # Subject can be set in your I18n file at config/locales/en.yml
  # with the following lookup:
  #
  #   en.order_mailer.shipped.subject
  #
  def shipped
    @greeting = "Hi"

    mail to: "to@example.org"
  end
end
```


```ruby
OrderMailer.received(@order).deliver_later

OrderMailer.received(@order).deliver_later
```