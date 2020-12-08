

https://github.com/wildbit/postmark-rails/wiki/Getting-Started



https://github.com/wildbit/postmark-rails/wiki/Using-Postmark-with-Devise-gem




```
bin/rails generate mailer User confirmation_instructions email_changed password_change reset_password_instructions unlock_instructions

```



 config/initializers/devise.rb
 ```
 config.mailer = 'UserMailer'
 ```





```
 class UserMailer < Devise::Mailer
  include PostmarkRails::TemplatedMailerMixin
  helper :application
  include Rails.application.routes.url_helpers
  include Devise::Controllers::UrlHelpers

  default from: 'no-reply@smartciti.es'
  #default reply_to: 'support@hammer-lane-industries.com' # Optional

  def confirmation_instructions(record, token, opts={})
    @admin = record
    @token = token
    # this will pass the data via the postmark-api to your template / layout these fields are 100% customizable and can be cahnged in your template / layout
    self.template_model = { product_name: 'your product',
                            username: @user.username,
                            email: @user.email,
                            confirmation_url: user_confirmation_url(@resource, confirmation_token: @token, subdomain: 'add subdomain here if needed'),
                            login_url: login_root_url(subdomain: 'add subdomain here if needed'),
                            trial_length: '14-days',
                            sender_name: 'What ever you want',
                            action_url: user_confirmation_url(@resource, confirmation_token: @token, subdomain: 'add subdomain here if needed'),
                            parent_company_name: 'Your company name',
                            company_address: 'Your address'}
    mail to: @admin.email, postmark_template_alias: 'devise_user_confirmation'

    # Rinse and Repeat for Password resets and Unlocks --- Ill update this gist with passowrd and unlocks in the near future
  end

  # def hello
  #   mail(
  #     :subject => 'Hello from Postmark',
  #     :to  => 'receiver@example.com',
  #     :from => 'sender@example.com',
  #     :html_body => '<strong>Hello</strong> dear Postmark user.',
  #     :track_opens => 'true'
  #   )
  # end

  # Subject can be set in your I18n file at config/locales/en.yml
  # with the following lookup:
  #
  #   en.user_mailer.confirmation_instructions.subject
  #
  def confirmation_instructions(record, token, opts = {})
    self.template_model = {
      action_url: edit_password_url(record, reset_password_token: token),
      user_email: record.email,
      # ... etc.
    }
    @email =
    mail to: record.email
  end

  # Subject can be set in your I18n file at config/locales/en.yml
  # with the following lookup:
  #
  #   en.user_mailer.email_changed.subject
  #
  def email_changed
    @greeting = "Hi"

    mail to: "to@example.org"
  end

  # Subject can be set in your I18n file at config/locales/en.yml
  # with the following lookup:
  #
  #   en.user_mailer.password_change.subject
  #
  def password_change
    @greeting = "Hi"

    mail to: "to@example.org"
  end

  # Subject can be set in your I18n file at config/locales/en.yml
  # with the following lookup:
  #
  #   en.user_mailer.reset_password_instructions.subject
  #


  def reset_password_instructions(record, token, opts = {})
    self.template_model = {
      action_url: edit_password_url(record, reset_password_token: token),
      user_email: record.email,
      # ... etc.
    }

    mail to: record.email
  end

  # Subject can be set in your I18n file at config/locales/en.yml
  # with the following lookup:
  #
  #   en.user_mailer.unlock_instructions.subject
  #
  def unlock_instructions
    @greeting = "Hi"

    mail to: "to@example.org"
  end
end

```




```
class User
	# ....

  def devise_mailer
    UserMailer # Must match your mailer class
  end
end

```