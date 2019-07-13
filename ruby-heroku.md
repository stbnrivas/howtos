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

```bash
# Procfile for rails
web: bundle exec puma -C config/puma.rb

#Procfile for rack app
web: bundle exec puma config.ru -p $PORT
```

```bash
heroku login
heroku create
#Creating app... done, ⬢ 

heroku git:remote -a frozen-cove-93893


git push heroku
heroku run rake db:migrate
heroku open
```

special deployment stuff

```bash
# for deploy not master branch to do:
`git push heroku testbranch:master`
# for deploy a subfolder to do:
`git subtree push --prefix $folder heroku master`
```


download the code from heroku

```bash
heroku git:clone -a $app_name
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

## heroku exec (ssh tunneling)

```bash
heroku ps:exec
```

## connection to database

```bash
heroku psql
```


## heroku deploy a subfolder

```bash
dnf install git-subtree
git subtree push --prefix src heroku master
```


## heroku accounts

https://github.com/heroku/heroku-accounts


- Installation

    $ heroku plugins:install heroku-accounts

- Usage

To add accounts:

    $ heroku accounts:add personal
    Enter your Heroku credentials.
    Email: david@heroku.com
    Password: ******

To add single sign-on (SSO) accounts:

    $ heroku accounts:add work --sso
    Enter your organization name: my-company-name
    Opening browser for login... done
    Enter your access token (typing will be hidden): **********************************

To switch to a different account:

    $ heroku accounts:set personal

To list accounts:

    $ heroku accounts
    * personal
    work

To find current account:

    $ heroku accounts:current
    personal

To remove an account:

    $ heroku accounts:remove personal
    Account removed: personal






## heroku addons: redis

first is a require a billing credit card

```bash
heroku addons
heroku addons | grep heroku-redis # check if redis was provisioned

heroku addons:create heroku-redis:hobby-dev

heroku addons:info # Use heroku addons:info redis-cool-1353667 to check 
heroku addons:docs heroku-redis # Use heroku addons:docs heroku-redis to view documentation

heroku config | grep redis
```

sharing heroku redis between applications

```bash
heroku addons:attach source-app-with-redis::REDIS --app destination-app-to-access-redis
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








heroku ps                       List the dynos for an app                                  Scaling
Start worker dynos. (Look at your Procfile to see the worker process types that are defined for your app)   heroku ps:scale worker=2    Scaling
Stop a particular dyno type *   heroku ps:stop worker   Scaling
Stop a particular dyno *    heroku ps:stop worker.2     Scaling
Restart all dynos   heroku ps:restart   Dyno Manager
Restart a particular dyno type  heroku ps:restart web   Dyno Manager
Restart a particular dyno   heroku ps:restart web.1     Dyno Manager
Scale horizontally (Add more dynos)     heroku ps:scale web=2   Scaling
Scale horizontally by incrementing the current number of dynos  heroku ps:scale web+5   Scaling
Scale different dyno types horizontally at the same time    heroku ps:scale web=1 worker=5  Scaling
Scale vertically (Use bigger dynos)     heroku ps:resize worker=standard-2x     Dyno Types
Scale horizontally and vertically at the same time. This example scales the number of web dynos to 3 and resizes them to performance-l  heroku ps:scale web=3:performance-l     Dyno Types
Get help for the heroku ps command  heroku ps --help    
Launch a one-off dyno that runs bash in a console   heroku run bash     One-Off Dynos
Launch a one-off dyno that runs the “worker” process type that is present in your application’s Procfile    heroku run worker   One-Off Dynos
View logs   heroku logs or heroku logs --tail   Logging