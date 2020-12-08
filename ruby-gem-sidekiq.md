# sidekiq

```ruby
require 'sidekiq'

Sidekiq.configure_client do |config|
  config.redis = {db: 1}
end

Sidekiq.configure_server do |config|
  config.redis = {db: 1}
end

class Worker
  include Sidekiq::Worker

  def perform(complexity)
    case complexity
    when 'hard'
      sleep 20
    when 'normal'
      sleep 5
    else
      sleep 1
    end
  end

end
```

```bash
bundle exec sidekiq -r ./sidekiq_test.rb
this launch a server

another terminal
bundle exec irb -r ./sidekiq_test.rb
Worker.perform("hard")
Worker.perform_in(5,"hard")
Worker.perform_async("hard")
```
IMPORTANT sidekiq is going to automatically retry the job that fail



```bash
require 'sidekiq'
require 'rack'
require 'sinatra'

Sidekiq.configure_client do |config|
  config.redis = {db: 1}
end

Sidekiq.configure_server do |config|
  config.redis = {db: 1}
end

require 'sidekiq/web'

class Worker
  include Sidekiq::Worker
  sidekiq_options retry: 0

  def perform(complexity)
    case complexity
    when 'hard'
      sleep 20
    when 'normal'
      sleep 5
    else
      sleep 1
    end
  end
end
```



```ruby
# config.ru

Sidekiq.configure_client do |config|
  config.redis = {db: 1}
end

require 'sidekiq/web'
run Sidekiq::Web
```ruby

```bash
sidekiqctl stop
```


you can launch into procfile a web and worker into same heroku dyno

Procfile
web: bundle exec rails server -p $PORT
worker: bundle exec sidekiq -e production

heroku ps:scale worker=1
