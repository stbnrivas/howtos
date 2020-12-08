# gem to check

act_as_list             manage objects with position
will_paginate           pagination
exception_notification  send email when errors occur
paperclip               manage files uploaded via web forms
carrierwave             manage files uploaded via web forms
shrine                  Shrine is a toolkit for file attachments in Ruby applications
dropzone                JS File upload by Matias Meno, to the Rails Asset pipeline.

delayed_job             queue task to run later
friendly_id             semantic URL
activemerchant          credit card processing


figaro					allow save key like twitter_api twitter_secret into yaml that is .gitignore and recover into the app using ENV["twitter_api"]




active_model_serializers	json serializer



rspec-rails

faker					a gem for generation of names, address ....

factory_bot 			is a fixtures replacement with a straightforward definition syntax, support for multiple build strategies
factory_bot_rails


mailcatcher				for emails send and view



## ecommerce en rails usando solidus

- spree (deprecated)
- solidus
- gem 'active_merchant'

es un fork de spree 2.4

solidus.io
modulo core, api, backend, frontend


integraciones con pasarelas de pago


para añadir solidus a un rails

gem solidus
gem solidus_auth_devise

bundle exec rails g spree:install
bundle exec rails g solidus:auth:install
bundle exec rake railties:install:migrations

bundle exec g solidus:views:override


en un rails engine??


con que version de rails funciona

pasarelas de pago

solidus.io
github.com/solidusio/solidus
guides.solidus.io/developers


gem active_merchant