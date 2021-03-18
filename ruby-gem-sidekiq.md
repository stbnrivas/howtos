# sidekiq without rails

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






## sidekiq into rails app


```bash
bundle add sidekiq

bin/rails generate sidekiq:worker hard

bin/rails generate sidekiq:worker context/hard
```


```ruby
# NOT NEEDED????''

# config/initializers/sidekiq.rb
Sidekiq.configure_server do |config|
  config.redis = { url: ENV.fetch("REDIS_URL") }
end

Sidekiq.configure_client do |config|
  config.redis = { url: ENV.fetch("REDIS_URL") }
end
```


```
class Context::HardWorker
  include Sidekiq::Worker

  def perform(*args)
    # Do something
  end
end

```


```bash
# start rails console
bin/rails c

```

```ruby
# create new works
HardWorker.perform_async()
#=> "b5f682066e12960e79b8bde8"

HardWorker.perform_in(5.minutes, 'some')
HardWorker.perform_at(5.minutes.from_now, 'some')
```

```bash
# check redis
redis-cli

KEYS *
#1) "queue:default"
#2) "queues"

```



```bash
# run the worker
bundle exec sidekiq
```



## run the web UI for sidekiq

```ruby
# gemfile
gem 'rack'
gem 'sinatra'
```

```ruby
# config.ru

require 'sidekiq'

Sidekiq.configure_server do |config|
  config.redis = { url: "redis://localhost:6379/0" }
end

require 'sidekiq/web'
run Sidekiq::Web
```

```
rackup config.ru
```



## remove all jobs into sidekiq

```ruby
require 'sidekiq/api'

# 1. Clear retry set

Sidekiq::RetrySet.new.clear

# 2. Clear scheduled jobs 

Sidekiq::ScheduledSet.new.clear

# 3. Clear 'Processed' and 'Failed' jobs

Sidekiq::Stats.new.reset

# 3. Clear 'Dead' jobs statistics

Sidekiq::DeadSet.new.clear

# Stats

stats = Sidekiq::Stats.new
stats.queues
# {"production_mailers"=>25, "production_default"=>1}

# Queue

queue = Sidekiq::Queue.new('queue_name')
queue.count
queue.clear
queue.each { |job| job.item } # hash content


# Redis Acess

Sidekiq.redis { |redis| redis.keys }
# ["stat:queues"...
```