# ruby on rails with mongodb


## STEP 1 - rails installation

rails with:
- skip activerecord
- skip test we will use rspec
- skip-action-mailbox
- skip-action-text - skip-active-storage
- skip-action-cable

```
rails new mongorails \
  --skip-active-record \
  --skip-bundle \
  --skip-test \
  --skip-system-test \
  --skip-action-mailbox \
  --skip-action-text \
  --skip-active-storage \
  --skip-action-cable \


cd mongorails
bundle add mongoid
bundle install

bin/rails g mongoid:config

	create  config/mongoid.yml

bundle add dotenv-rails
```


## STEP 3 - configure your .env

```
# .env

DB_HOST=127.0.0.1
DB_PORT=5432

DB_NAME_DEV=db_deb
DB_USER_DEV=postgres
DB_PASS_DEV=secret

DB_NAME_TEST=db_test
DB_USER_TEST=postgres
DB_PASS_TEST=secret

# heroku database integration
# DATABASE_URL=postgres://USER:PASS@HOSTNAME:PORT/DATABASE
# DATABASE_URL=postgres://postgres:secret@127.0.0.1:5432/dbname
```


## STEP 4 - use your .env file into config/mongoid.yml

mongoid can connect using

- uri: uri: mongodb://user:password@mongodb.domain.com:27017/frontend_development
- via multiples params host, database, options (user, password, roles, auth_source)

original file config/mongoid.yml is
```
development:
  clients:
    # Defines the default client. (required)
    default:
      # Mongoid can connect to a URI accepted by the driver:
      # uri: mongodb://user:password@mongodb.domain.com:27017/frontend_development

      # Otherwise define the parameters separately.
      # This defines the name of the default database that Mongoid can connect to.
      # (required).
      database: database: mongorails_development
      hosts:
        - localhost:27017
      options:
  # Configure Mongoid specific options. (optional)
  options:

test:
  clients:
    default:
      database: mongorails_test
      hosts:
        - localhost:27017
      options:
        read:
          mode: :primary
        max_pool_size: 1
```

modified file in config/mongoid.yml

```
development:
  clients:
    default:
      database: <%= ENV.fetch("DB_NAME_DEV")%>
      hosts:
      - <%= ENV.fetch("DB_HOST")%>:<%= ENV.fetch("DB_PORT")%>
      options:
        user: <%= ENV.fetch("DB_USER_DEV")%>
        password: <%= ENV.fetch("DB_PASS_DEV")%>
        roles:
        - 'dbOwner'
        auth_source: admin
  # Configure Mongoid specific options. (optional)
  options:
test:
  clients:
    default:
      database: <%= ENV.fetch("DB_NAME_TEST")%>
      hosts:
      - <%= ENV.fetch("DB_HOST")%>:<%= ENV.fetch("DB_PORT")%>
      options:
        user: <%= ENV.fetch("DB_USER_TEST")%>
        password: <%= ENV.fetch("DB_PASS_TEST")%>
        roles:
        - 'dbOwner'
        auth_source: admin
  # Configure Mongoid specific options. (optional)
  options:
production:
  clients:
    default:
      uri: mongodb://<%= "#{ENV.fetch('DB_USER_DEV')}:#{ENV.fetch('DB_PASS_DEV')}@#{ENV.fetch('DB_HOST')}:#{ENV.fetch('DB_PORT')}/#{ENV.fetch('DB_NAME_DEV')}"%>
    options:

```


## STEP 5 - run a mongodb container as database

```
docker pull mongo:4.4-bionic

cd mongorails
source .env

#attaching to shell:
docker run    --name mongodb -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=${DB_PASS_DEV} -e MONGO_INITDB_ROOT_PASSWORD=${DB_PASS_DEV} mongo:4.4-bionic

```


## STEP 6 - test if works using scaffold


```
bin/rails g scaffold Thing uid:string lat:string lon:string utc:string
```



## STEP 6 - adding authentication with sorcery with simple password


```
bundle add sorcery

bin/rails g sorcery:install

      create  config/initializers/sorcery.rb
    generate  model User --skip-migration
       rails  generate model User --skip-migration
      invoke  mongoid
      create    app/models/user.rb
      insert  app/models/user.rb


# user_activation, reset_password, remember_me, session_timeout, brute_force_protection, http_basic_auth, activity_logging, external

rails generate sorcery:install


rails g scaffold_controller user email:string crypted_password:string salt:string

```







adding rspec

```
bundle add rspec
```


