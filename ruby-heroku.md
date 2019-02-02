# heroku cli installation

```bash
sudo dnf install snapd
# simbolic link for fedora
sudo ln -s /var/lib/snapd/snap /snap

sudo snap install --classic heroku
```

check if installed

```bash
/snap/bin/heroku help
```

add snap path to system path
```bash
vi ~/.bash_profile
# export PATH="$PATH:/snap/bin/"
```

# heroku deploy project

you must have a git project with a branch master, only the branch master will
configure as herokuapp

your project must to have a file with name Procfile with this content for ruby on rails

```
web: bundle exec puma -C config/puma.rb
```

```bash
heroku login
heroku create
git push heroku
heroku run rake db:migrate
heroku open
```

## utils in heroku

```bash
cd herokuapp
heroku logs --tail
heroku ps
```

```bash
heroku config

# DATABASE_URL:             postgres:// ...
# LANG:                     en_US.UTF-8
# RACK_ENV:                 production
# RAILS_ENV:                production
# RAILS_LOG_TO_STDOUT:      enabled
# RAILS_SERVE_STATIC_FILES: enabled
# SECRET_KEY_BASE:         a28...
heroku config:set RACK_ENV='development'
heroku config:set RAILS_ENV='development'

heroku config:set RACK_ENV='production'
heroku config:set RAILS_ENV='production'
```

```bash
heroku run bash
heroku run rails console
```




## heroku addons: sendgrid (verifyed account)

```bash
heroku addons:create sendgrid:starter
heroku config:get SENDGRID_USERNAME
heroku config:get SENDGRID_PASSWORD
```

Obtaining an API key



# heroku hosting service free

heroku works with free dyno, this proccess server your herokuapp. Every 30 minutes without activity dyno will sleep

- free dyno (sleep after 30 minutes)
- hobby dyno (you must add credit card)

```bash
heroku ps
```

Free dyno hours quota remaining this month: 544h 1m (98%)
Free dyno usage for this app: 5h 23m (0%)
For more information on dyno sleeping and how to upgrade, see:
https://devcenter.heroku.com/articles/dyno-sleeping

=== web (Free): bundle exec puma -C config/puma.rb (1)
web.1: up 2019/01/31 10:30:14 +0100 (~ 13m ago)
