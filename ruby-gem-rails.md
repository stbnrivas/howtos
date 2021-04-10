# ruby on rails stuff

railties:

Before you can actually set up this web server, there are quite a few things that need to be configured. Railties are the engines for reading these configurations, creating an application, and connecting different parts of Rails. All major components of Rails are created as a subclass of Rails::Railtie. For example, Active Record and Action Controller.


ruby on rails is composed by:
- ActiveRecord (Model)
- ActionView (View)
- ActionController (Controller)

all are packed into ActionPack

others components/gems of rails:
- turbolinks: This gem contains a Rails engine which integrates seamlessly with the Rails asset pipeline. it is for use ajax transparently

- jbuilder


## ruby on rails new app creation

```bash
gem list --local rails
gem install rails -v 6.0.1

rails _6.0.1_ --version
rails _6.0.1_ new $new_project
```


```bash
mkdir $new_project && cd && rails new .
rails new $new_project --database sqlite
rails new $new_project --database mysql
rails new $new_project --database postgresql

rails new $new_project --webpack=vue
```

## flags in rails new

```bash
rails _5.2.1_ new my-cool-rails-app

rails new \
  --skip-spring \
  --skip-action-mailer \
  --skip-action-mailbox \
  --skip-action-text \
  --skip-active-record \
  --skip-active-storage \
  --skip-puma \
  --skip-action-cable \
  --skip-listen \
  --skip-sprockets \
  --skip-javascript \
  --skip-turbolinks \
  --skip-test \
  --skip-system-test \
  --skip-bootsnap \
  --skip-webpack-install \
  my-cool-rails-app
```

```bash
rails new --api

rails new --minimal
```

```bash
rails new cool_app --minimal
rails new cool_app --minimal webpack=react works

# A minimal rails stack to get you started, everything that is excluded:
#    skip_action_cable
#    skip_action_mailbox
#    skip_action_mailer
#    skip_action_text
#    skip_active_job
#    skip_active_storage
#    skip_bootsnap
#    skip_jbuilder
#    skip_spring
#    skip_system_tests
#    skip_turbolinks
#    skip_webpack
# Sprockets should have JavaScript folders by default

```

## check errors and currents version for existing app

```bash
bin/rails about
```


## error add domain to config host 

Error: Blocked host

```ruby
# config/environments/{development,production}.rb
Rails.application.configure do
  # config.hosts = nil
  config.hosts = "yourcooldomain.com" # static
  config.hosts = ENV.fetch("DOMAIN")  # dinamically by .env
end

```



## running rails

```bash
# only within the host
bin/rails server
```

```bash
# all host into the same network
bin/rails server -b 0.0.0.0

cat 'config.hosts.clear' >> config/enviroments/development
```

```bash
yarn install
# into production environment
RAILS_ENV=production bin/rails assets:precompile

bin/rails server -e production
```



## change database for installed rails

```bash
bin/rails db:system:change --to=mysql
```




## configuration for load

```bash
bin/rails runner 'p ActiveSupport::Dependencies.autoload_paths'
```


```ruby
# config/enviroment/development.rb
config.autoload_paths += %W(#{Rails.root}/app/services)
```

```ruby
# config/application.rb
config.autoload_paths += %W(#{Rails.root}/app/services)
```


## create database in mysql

```bash
mysql -u root -p
```
database creation & user creation & grant privileges to user to database

```sql
CREATE DATABASE $database_developments;
GRANT ALL PRIVILEGES ON $database_development.* TO '$user_development'@'localhost' IDENTIFIED BY '$password_developer';
CREATE DATABASE $database_test;
GRANT ALL PRIVILEGES ON $database_test.* TO '$user_test'@'localhost' IDENTIFIED BY '$password_test';

SHOW DATABASES;
CREATE DATABASE $database_development;
USE $database_development;
DROP DATABASE $database_development;
```
change rails configuration to set database $project_folder/config/database.yml

```yml
default: &default
  adapter: mysql2
  encoding: utf8
  pool: 5
  username: $user_development
  password: $password_developer
  #socker: /tmp/mysql.sock
  host: localhost

development:
  <<: *default
  database: $database_development
```


```bash
rails db:schema:dump
bin/rails db:drop
bin/rails db:fixtures:load
bin/rails db:seed
bin/rails db:create
bin/rails db:migrate:status
bin/rails db:migrate:down VERSION=2019014486
bin/rails db:migrate:up VERSION=2019014486
bin/rails db:drop
```

```bash
```

```bash
rails server
# you don't need restart the webserver unless you change configuration
ctrl + c
```

## create database in postgresql

```bash
mkdir railspg ; cd railspg ; mkdir db
rails new src --database postgresql
touch docker-compose.yml
```

create container manually from CLI

```bash
docker container run --interactive --tty --publish 5432:5432 --mount type=bind,source=$(pwd)/db,destination=/var/lib/postgresql/data postgres:11.1
```

```powershell
docker container run --interactive --tty --publish 5432:5432 postgres:11.1
```

THERE A FUCKING PROBLEM WHEN TRY MOUNT THE VOLUME INTO WINDOWS 10 CONTAINER:

running bootstrap script ... 2019-01-01 01:04:46.190 UTC [76] FATAL:  data directory "/var/lib/postgresql/data" has wrong ownership
2019-01-01 01:04:46.190 UTC [76] HINT:  The server must be started by the user that owns the data directory.
child process exited with exit code 1



create container using docker-compose.yml

```yml
version: '3'
services:
  dbpgrails:
    image: "postgres:11.1"
    volumes:
    - ./db:/var/lib/postgresql/data
    ports:
      - "5432:5432"
```




```bash
psql -h postgres -U postgres
```

```bash
rails server
```


```bash
# convention: the name controller used in generator should always go in Plural
# convention: should use camel case to named controller ParkingSpot or Parking_Spot
rails generate
rails generate controller
rails generate controller $name_controller $action
rails generate controller demo index

 rails generate controller demo index
      create  app/controllers/demo_controller.rb
       route  get 'demo/index'
      invoke  erb
      create    app/views/demo
      create    app/views/demo/index.html.erb
      invoke  test_unit
      create    test/controllers/demo_controller_test.rb
      invoke  helper
      create    app/helpers/demo_helper.rb
      invoke    test_unit
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/demo.coffee
      invoke    scss
      create      app/assets/stylesheets/demo.scss
```

```bash
# you can push controller into subfolder to group diferent controlles

rails g controller API::Events
```


```bash
rails destroy model $model_name
rails destroy controller $controller_name
```










## routing

controller can be:
 - resource based (use resource in routes)
 - action based (don't use resource in routes)


```ruby
# config/routes.rb
Rails.application.routes.draw do
  # simple route
  get 'demo/index'
  match "demo/index", :to => "demo#index", :via => :get
  # default route, may go away in future versions of rails
  get ':controller(/:action(/:id))'
  match ':controller(/:action(/:id))', :via => :get
  # root route
  root "demo#index"
  match "/", :to => "demo#index", :via => :get
  # resourceful routes
end
```

## render template

```ruby
# into controller
render(:template => 'demo/hello')
render('demo/hello')
render('hello')
render(:partial => 'form')
render(:partial => 'other_controller/form')
render(:partial => 'other_controller/form',:locals => {:var => 'value'})
```

## redirect action

```ruby
redirect_to(:controller => 'demo', :action => 'index')
redirect_to(:action => 'index')
redirect_to("http://example.org")
```

## links

```ruby
link_to('click to go',{:controller => 'demo',:action => 'index'})
# /demo/hello/1?page=2&pagination=10
link_to('click',{:controller=>'demo',:action=>'index',:id => 2,:page=>2,:pagination=>10})
```

model_path vs model_url

```ruby
product_url(product)
# => https://domain.com/products/1
# use for redirect_to
redirect_to 'see more', product_url(product)


product_path(product)
# => /product/1
# user for link_to
link_to 'see more', product_path(product)
```




## databases

config/database.yml
rails db:schema:dump

```bash
rails generate migration MigrationNameCamelCase
rails generate
```

```ruby
class DoNothingYet < ActiveRecord::Migration[5.2]
#  def change
#  change method is a shorthand for separete methods
#  end

  def up
  end

  def down
  end

end
```


```bash
# convention: the name model used in generator should always go in singular
# convention: User is model and Users will be the table
rails generate model ModelNameCamelCaseSingular
rails generate model User

rails destroy model ModelNameCamelCaseSingular
rails destroy model User
```
 invoke  active_record
      create    db/migrate/20190101191154_create_users.rb
      create    app/models/user.rb
      invoke    test_unit
      create      test/models/user_test.rb
      create      test/fixtures/users.yml

```ruby
class CreateUsers < ActiveRecord::Migration[5.2]
  def up
    create_table :users do |t|
      t.column "first_name", :string
      t.string "last_name"
      t.string "email", :default => '', :null => false

      # t.datetime "created_at"
      # t.datetime "updated_at"
      # or shortcut
      t.timestamps

      # t.column "value", :binary
      # t.column "value", :boolean
      # t.column "value", :date
      # t.column "value", :datetime
      # t.column "value", :decimal
      # t.column "value", :float
      # t.column "value", :integer
      # t.column "value", :string
      # t.column "value", :text
      # t.column "value", :time

      # t.column "value", :string, :limit => size
      # t.column "value", :string, :default => value
      # t.column "value", :string, :null => true/false

      # t.column "value", :decimal, :precision => number
      # t.column "value", :decimal, :scale => number

      t.timestamps
    end
  end

  def down
    drop_table :users
  end

end
```

```bash
rails db:migrate
rails db:rollback

rails db:migrate VERSION=0
rails db:migrate:status
rails db:migrate:up VERSION=20190101190412
rails db:migrate:down VERSION=20190101190412
rails db:migrate:redo VERSION=20190101190412
# redo is first down and after up again
```


column migration method
```ruby

create_table :table_name do |t|
end
rename_table("table","new_name")


add_column(table,column,type,options)
remove_column(table,column)

rename_column(table,column,new_name)
change_column(table,column,type,options)

add_index(:table,:column,{})
  options = {:unique => true, :name => "custom_name"}
remove_index(table,column)
```



## rails console

```bash
rails console development
rails console
rails c
```


```bash
person = Person.new
person.new_record?
if person.save
  puts "saved"
else
  puts "not saved"
end

person = Person.create(:name => '')
# returns person
puts "not saved " if person.nil?

person = Person.find(1)
person.save

person.update_attributes(:name => 'John')

person = Person.find(1)
person.destroy # remove from database but still exist in person variable as frozen, you can not modify

persons = Person.all
person = Person.first
person = Person.last

person = Person.where("name='Test' AND visible=true") # vulnerable to sqlinjection only with static never do dinamically
person = Person.where(["name=? AND visible=true","Test"]) # safe from sqlinjection and flexible
person = Person.where(:name => "Test",:visible => true) # safe from sqlinjection and flexible
# returns an ActiveRelation, which can be chained
persons = Person.where(:visible=> true).where(:first_name => 'John')
persons.to_sql


persons = Person.all.order(:position)
persons = Person.all.order(:position => :asc)
persons = Person.all.order(:position => :desc)
persons = Person.all.order("position")
persons = Person.all.order("position ASC")
persons = Person.all.order("position DESC")
persons = Person.where(:visible => true).limit(10)
persons = Person.where(:visible => true).offset(10)

persons = Person.where(:visible => true).limit(10)offset(40)

```

named scoped

  - queries defined in a model using ActiveRelation can accept params and requires lambda syntax

```ruby
scope :active, lambda {where(:active => true)}
scope :active, -> {where(:active => true)}
def self.active
  where(:active => true)
end

scope :with_content_type, lambda {|ctype|
  where(:content_type => ctype)
}
def self.with_content_type(ctype)
  where(:content_type => ctype)
end
section.with_content_type('html')

scope :recent, lambda {
  where(:created_at => 1.week.ago..Time.now)
}
```


## relationship: rails associations


### relation 1:1
:has_one, :belongs_to foreign key are at same model that has belongs_to

```ruby
class Link < ApplicationRecord
  belongs_to :page #,{ :foreign_key => 'page_id'}
  # belongs_to is not optional by default, error if you try save
  # to disable:
  belongs_to :page, {:optional => true}
end

class Page < ApplicationRecord
  has_one :link
end

link.page
page.link
```


### relation 1:M
:has_many, :belongs_to foreign key are at same model that has belongs_to

```ruby
class Page < ApplicationRecord
  have_many :paragraph
end
class Paragraph < ApplicationRecord
  belongs_to :page
end

page.paragraphs
page.paragraphs = [paragraph, paragraph, paragraph]
paragraph.page

page.paragraphs.delete(paragraph)
page.paragraphs.destroy(paragraph)
page.paragraphs.clear
page.paragraphs << paragraph
```


### relation M:N (Simple)
:has_and_belongs_to_many, :has_and_belongs_to_many

requires a join table, two foreign keys
name for join table will be plural and name for sort name is alphabetical

Page & Tag  -> Pages_Tags

```ruby
class Page < ApplicationRecord
  has_and_belongs_to_many :tags #, :join_table => 'pages_tags'
end
class Tag < ApplicationRecord
  has_and_belongs_to_many :pages
end
```

migration file

```ruby
class CreatePagesTagsJoin < ActiveRecord::Migration[5.0]
  def up
    create_table :pages_tags, :id => false do |t|
      t.integer "page_id"
      t.integer "tag_id"
    end
    add_index("idx_pages_tags",["page_id","tag_id"])
  end

  def down
    drop_table :pages_tags
  end
end
```

```ruby
page = Page.create(:title => 'title 1')
tag = Tag.create(:name => 'tag name 1')

page.tags << tag
```


### relation M:N (Rich)
names of join table usually end -ments, -ships


Courses (C++,C,Java,Ruby)
Students (Jane Doe, John Doe)

and you need save calification for example

```bash
rails generate model CourseEnrollment
```

```ruby
def up
  create_table :courses_enrollments do |t|
    t.integer "course_id"
    t.integer "student_id"

    t.integer "calification"
  end
  add_index("idx_courses_enrollments",["course_id","student_id"])
end
def down
  drop_table :courses_enrollments
end
```


```ruby
class Course < ApplicationRecord
  has_many :enrollments #, :join_table => 'courses_enrollments'
end
class Student < ApplicationRecord
  has_many :enrollments
end

class CourseEnrollment < ApplicationRecord
  belongs_to :course
  belongs_to :student
end
```


TODO: has_many :throught



## CRUD

/model/new
/model/create

/models
/model/show/:id

/model/edit/:id
/model/update/:id

/model/delete/:id
/model/destroy/:id

controller must be in plural like, UsersConstroller, PagesController



```bash
bin/rails generate controller --help
# rails generate controller NAME [action action] [options]


# we will use generator
# controller word ever use plural
bin/rails generate controller Pages index show new edit delete

bin/rails generate controller MultiWords index show new edit delete
bin/rails generate controller multi_words index show new edit delete

bin/rails generate controller api/v1/authors index show
bin/rails destroy  controller api/v1/authors index show


bin/rails generate controller api/v1/parking_spots index show
bin/rails destroy  controller api/v1/parking_spots
```

rest paradigm requirements

- GET
- POST
- PATCH
- DELETE

```ruby
# config/routes

resources :pages
resources :pages, :except =>[:show,:index]
resources :pages, :only =>[:index]

resources :pages do
  member do
    get :delete
  end

  collection do
    get :export
  end
end
```

```bash
rails routes
```

resourceful URL helpers

GET     /pages              pages_path
GET     /pages/:id          page_path(:id)
GET     /pages/new          new_page_path
POST    /pages              pages_path
GET     /pages/:id/edit     edit_page_path(:id)
PATCH   /pages/:id          page_path(:id)
GET     /pages/:id/delete   delete_page_path(:id)
DELETE  /pages/:id          subject_path(:id)


<%= link_to('all pages', pages_path)%>
<%= link_to('all pages', pages_path(:page=>3))%>
<%= link_to('show pages', page_path(@page.id))%>
<%= link_to('show pages', page_path(@page.id,:format => 'verbose'))%>
<%= link_to('edit pages', edit_page_path(@page.id))%>



## scaffolding

```bash
bin/rails generate scaffold --help
# rails generate scaffold NAME [field[:type][:index] field[:type][:index]] [options]


bin/rails generate scaffold post title:string body:text published:boolean
bin/rails generate scaffold purchase amount:decimal tracking_id:integer:uniq
bin/rails generate scaffold user email:uniq password:digest

bin/rails generate destroy user email:uniq password:digest
```

```bash
bin/rails generate scaffold_controller --help

bin/rails g scaffold_controller user email:string crypted_password:string salt:string
```

## strong parameters into

```ruby
Subject.new(params[:subject])
Subject.create(params[:subject])
@subject.update_attributtes(params[:subject])

# error ActiveModel::ForbidenAttributtesError
params.permit(:first_name, :last_name)
params.require(:subject)
params.require(:subject).permit(:name,:position,:visible)

@subject.new(params.require(:subject).permit(:name,:position,:visible))
def subject_params
  params.require(:subject).permit(:name,:position,:visible)
end
# and you can use:
@subject.new(subject_params)
```


## flash hash

html is stateless, each request is distinct, no previous information. Cookies and session allow data between request.

flash hash stores message in session data
flash hash clears old messages after every request

```ruby
flash[:notice]  = "message"
flash[:error]  = "message"
```

## helpers

### text helpers

```ruby
word_wrap(:text, :line_width => 30)
# input:
# lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor 
# output:
# lorem ipsum dolor lorem ipsum dolor\n
# lorem ipsum dolor lorem ipsum dolor\n

simple_format(text)
# input:
# lorem ipsum dolor lorem ipsum dolor\n lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor 
# output:
# <p>lorem ipsum dolor lorem ipsum dolor<br>lorem ipsum dolor lorem ipsum dolor</p>

truncate(text, :length => 10)
# input:
# lorem ipsum dolor lorem ipsum dolor\n lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor 
# output:
# lorem ipsum dolor lorem

pluralize(n,'product')

truncate_words()
highlight()
excerpt()
```

### number_helpers

```ruby
  # :delimiter => 
  # :separator => 
  # :precision => 2-3
  # :unit =>

# number_to_currency
number_to_currency(34.5) # $34.50
number_to_currency(34.5, :precision => 0, :unit =>'kr',:format => "%n %u") # 35 kr

# number_to_percentage
number_to_percentage(34.5) # 34.500%
number_to_percentage(34.5, :precision =>1, :separator => ',') # 34,5%

# number_with_precision / number_to_rounded
number_with_precision(34.56789) # 34.568
number_with_precision(34.56789, :precision => 6) # 34.56890

# number_with_delimiter / number_to_delimited

# number_to_human
number_to_human(123456789) # 123 Million
number_to_human(123456789,:precision => 5) # 123.46 Million

# number_to_human_size
number_to_human_size(1234567) # 1.18Mb
number_to_human_size(1234567, :precision => 2) # 1.2Mb

# number_to_phone
number_to_phone(1234567890) # 123-456-7890
number_to_phone(1234567890, 
 :area_code => true,
 :delimiter => ' ',
 :country_code => 1,
 :extension => '321' ) 
# +1 (123) 456 7890 x 321
```


### DateTime Calculations using integers

- second | seconds
- minute | minutes
- hour | hours
- day | days
- week | weeks
- month | months
- year | years

```ruby
Time.now + 30.days - 23.minutes

30.days.ago # Time.now - 30.days
30.days.from_now # Time.now + 30.days
```

relative datetime calculations

- beginning_of_day        end_of_day
- beginning_of_week       end_of_week
- beginning_of_month      end_of_month
- beginning_of_year       end_of_year
- yesterday               yesterday
- last_week               next_week
- last_month              next_month
- last_year               next_year

```ruby
Time.now.last_year.end_of_month.beginning_of_day
```

### ruby DateTime Formatting

```ruby
datetime.strftime( format_string)
Time.now.strftime("%B %d, %Y %H.%M") 
# => "January 06, 2019, 13:40"
```

Day
%a    abbreviated Weekday name => Sun
%A    full weekday => Sunday
%d    numeric day of month => 01..31

Month
%b    abreviated month name
%B    full month name
%m    numberic month

Year
%y    year abreviated two digits
%Y    full year with four digits

Time
%H    hour in 24-hours format (00..23)
%I    hour in 12-hours format (01..12)
%M    minute (00..59)
%S    seconds (00..59)
%p    AM (ante meridiem: antes mediodia)
      PM (post meridiem: despues mediodia)
%Z    time zone


### rails datetime formating

```ruby
datetime.to_s(format_symbol)
datetime.to_s(:db)        "2019-01-09 14:00:00"
datetime.to_s(:number)    "20190109140000"
datetime.to_s(:time)      "14:00"
datetime.to_s(:short)     "09 Jan 14:00"
datetime.to_s(:long)      "January 09, 2019 14:00"
datetime.to_s(:ordinal)   "January 9th, 2019 14:00"
```

### custom helpers

the custom helpers are defined in ruby modules, and created when generates a controller into /app/helpers. There are available in views.
Are useful for frecuently or large sections of code. There are application_helper.rb into helpers foler

```ruby
module PagesHelper

  def slider(images,style,timeout)
    # return the html to use
  end

end
```

### sanitize helpers

to avoid Cross-Site Scripting (XSS)
to use with undesirable HTML
to escape all user-entered data, form parameter, cookie data, database data

```ruby
html_escape()
h()
raw()
html_safe()
```
from rails 3 all is escape from default the method h executed


### escape output

```ruby
# strip_links(html)
text = '<strong>Please visit</strong><a href="http://example.com"> us</a>'
strip_links(text) # <strong>Please visit </strong> us


# sanitize(html, options)
sanitize(html, 
  :tags => ['p','br','strong','em']
  :attributes => ['id','class','style'])
# use to avoid that into a text place holder add script o something that doesn't allow
```




## Asset Pipeline

- concatenate CSS and JS files into single file
- compress and minifies CSS and JS
- precompiles CSS and JS
- allow writing assets in other languages
- adds assets fingerprint

public/images         app/assets/images
public/javascript     app/assets/javascripts
public/stylesheets    app/assets/stylesheets

files in public directory are served exactly as-is without concatenation, compression or minification, you can not use sass, coffescript or erb and without fingerprint


the manifest files

- contain directives for including asset files
- loaded, processed, concatenated, compressed

development vs production

development: skips concatenation, skips compression, skips fingerprint, does file processing
production: assume assets have been precompiled


asset pipeline

public/assets/application-2312324k423weq234.css -> public/assets/application-2312324k423weq234.css.gz

```bash
export RAILS_ENV=production
bundle exec rails assets:precompile
```

### stylesheets  into assets pipeline

- write stylesheets
- list sytlesheet in manifest
- add manifest to assets precompile list
- include a stylesheet link tag in html

with assets pipeline app/assets/stylesheets/file.css.scss
without asset pipeline public/stylesheets/file.css

into file app/assets/stylesheets/application.css the manifest

require .
require primary
require_self


config/initializers/assets.rb

uncomment

Rails.application.config.assets.precompile += %w (admin.css main.css)

then you need change

# html
<link href="/assets/stylesheets/application.css" rel="stylesheets" type="text/css" media="all"/>

# rails helper

stylesheet_link_tag('application')


#### javascript in assets pipeline

- write js file
- list js files at manifest
- add manifest to assets precompile
- include into js tag at html

with asset pipeline app/assets/javascript
without asset pipeline public/javascript

files must end with .js .coffee

app/assets/javascript/application.js

//= require jquery
//= require jquery_ujs
//= require turbolinks
//= require tree .

//= require demo

config/initializers/assets.rb

application.js is in precompiled

html tag
<script src="/assets/javascript/application.js" type="text/javascript"></script>

rails helper
javascript_include_tag('application')

escape_javascript()
j()


### images into assets pipeline

with asset pipeline app/assets/images
without asset pipeline public/images

user-upload image will be into public/images if you need include images into assets pipeline can use gems like paperclip and carrierwave

html_tag
<img src="/assets/logo.png">

rails helper
image_tag('logo.png')
image_tag('logo.png', :size=> '90x55', :alt => 'logo' )

for images into scss or css files 

```scss
footer {
  // background: url('/assets/gradient.png')
  background: image-url('gradient.png')
}
```


#### form helpers

text_field
password_field
text_area
hidden_field
radio_button
check_box
file_field
label

```ruby
form_form(@subject, :html => {:multipart =>true}) do |f|
  f.label(:name)
  f.text_field(:name,:size => 40,:maxlength=>50)
  f.password_filed(:password, :size => 40)
  f.hidden_field(:token, 'abcde')
  f.text_area(:description, :size => '40x20')
  f.radio_button(:content_type, "text")
  f.radio_button(:content_type, "HTML")
  f.check_box(:visible)
  f.file_field(:logo)
```

form option helpers

```ruby
select(@boject,attribute,choices,options,html_options)
```
options
  :selected => object.attribute
  :include_blank => false
  :prompt => false
  :disabled => false

```ruby
form_for(@object) do |f|
  f.select(:position, 1..5)
  f.select(:content_type,['text','html'])
  f.select(:visible,{"visible"=>1,"hidden"=>2})
  f.select(:page_id,Page.all.map{|p| [p.name,p.id]})
end
```


#### date and time form helpers

date_select(object,attribute,options,html_options)

options = {
  :start_year => Time.now.year-5,
  :end_year => Time.now.year+5,
  :order => [:year,:month,:day],
  :discard_year => false,
  :discard_month => false,
  :discard_day => false,
  :include_blank => false,
  :prompt => false,
  :use_month_numbers => false,
  :add_month_numbers => false,
  use_short_month => false,
  date_separator => ""
}


### form errors

```ruby
validates_presence_of :name

object.errors # array containing any error added by validations
object.errors.clear
object.errors.size
object.errors.each { |attr,msg| }
# :name, "can't be blank"
object.errors.full_messages.each{|msg| ...}
# "name can't be blank
```

there are to ways of display errors
- list errors above the form
- print and highlight error with each form input

it's a good practise put error messages into a partial

```html
<% if object && object.errors.size > 0 %>
<div id="errors-explanation">
<h2><%=pluralize(object.errors.size, "error"%> prohibited this record </h2>
<ul>
  <% object.error.full_messages.each do |m| %>
  <li><%=m%></li>
  <% end %>
</ul>
</div>
```

into application_helper.rb

```ruby
module ApplicationHelper
  def error_messages(object)
    render(:partial => 'application/error_messages', :locals => {:object => object})
  end
end
```






### cross-site request forgery CSRF

authenticity toke is create when use form_form

into app/controllers/application_controller.rb

```ruby
class ApplicationController < ActionController::Base
  protect_form_forgery with: :exception
end
```

CSRF token for JS and Ajax

<%= csrf_meta_tag %>


### validation of models 

ensure data apply requirements before saving in database, resides into models

validates_presence_of           can not be nil, false, "", [], {}
  :message => "custom message"
validates_length_of
  :is
  :minimum
  :maximum,
  :within,
  :in

  :message => "custom message"
validates_numericality_of
  :equal_to
  :greather_than, :less_than, greather_than_or_equal_to, :less_than_or_equal_to
  :odd, :even, :only_integer
  :message => "custom message"
validates_inclusion_of
  :in
  :message => "custom message"
validates_exclusion_of
  :message => "custom message"
validates_format_of
  :with
validates_uniqueness_of
  :case_sensitive
  :scope
validates_acceptance_of
validates_confirmation_of
validates_associated



options = {
  # only check validation :on ...
  :on => :save,
  :on => :create,
  :on => :update,
  # if method return true or false
  :if => :method,
  :unless => :method,
}


model.valid?
model.errors
model.errors.full_messages

validates methods can join all validation for single attribute into single method

```ruby
class CustomModel < ApplicationRecord

  EMAIL_REGEX = /\A[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}\Z/i

  validates_presence_of :email
  validates_length_of :email, :maximum => 50
  validates_uniqueness_of :email
  validates_format_of :email, :with => EMAIL_REGEX
  validates_confirmation_of :email
end


# validates :attribute, 
#     :presence => boolean,
#     :numericality => boolean,
#     :length => options_hash,
#     :format => {:with => regex},
#     :inclusion => {:in => array_or_range},
#     :exclusion => {:in => array_or_range},
#     :acceptance => boolean,
#     :uniqueness => boolean,
#     :confirmation => boolean,

class CustomModel < ApplicationRecord

  EMAIL_REGEX = /\A[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}\Z/i

  validates :first_name, :presence => true, :length => {:maximum =>25}
  validates :email, :presence => true,
    :length => {:maximum => 100},
    :format => EMAIL_REGEX,
    :confirmation => true
end
```



### custom validations


```ruby
class CustomModel < ApplicationRecord
  validate :custom_validation

  private
  def custom_validation
    errors.add(:attribute,"custom message, not implemented!!")
  end
end
```



## cookies and sessions

cookies in rails are a hash, maximum data size 4k ~ 4000 characters, reside on user client, and can be deleted, read or altered

```ruby
cookies[:username] = "johnDoe"
cookies[:username] = {
  :value => "john doe",
  :expires => 1.week.from_now
}
```

sessions, web server sends a session ID to the browser, which then saves it in a cookie
browser sends session ID with each future request to tha web server
web server use session ID to locate the session file

```ruby
session[:username] = "johnDoe"
```

session require tiem to retrieve the session file
session files accumulate
session cookie resides on the user's computer can be deleted or hijacked
session storage on the server can be:
- in files 
- database storage
- cookie storage (default since rails 3) fast no lookup needed, no setup, encrypted to prevent reading, signed to prevent tampering 4K maximum size


configurable at 
- config/initializers/session_store.rb
- config/secrets.yml




## controller filters

execute code before or after a controller action like a callback
- filter request before allowing actions
- remove code repetition (set variables, find database, get shop card)

before_actions
after_action
around_action

```ruby
class SomeController <  ApplicationController
  before_action :find_subjects, only => [:show]
  before_action :find_subjects, except => [:new]

  def show
    # ...
  end

  private
  def find_subjects
    @subjects = Subjects.sorted
  end
end
```

filter methods should be declared private
any render or redirect before an actoin prevents its execution, the action will not executed
filters in ApplicationController are inherited by all controllers
inhterited filters can be skipped
  skip_before_action
  skip_after_action
  skip_around_action



### server logs, application logs

log/development.rb
log/production.rb
log/test.rb

log level configuration can be configured at

config/environments/development.rb
config.log_level = :debug
config/envirionments/production.rb
config.log_level = :info

logs level:
:debug, :info, :warn, :error, :fatal


```bash
bin/rails log:clear
bin/rails log:clear LOGS=test
```


```ruby
logger.debug("*** ***")
logger.info("")
logger.warn("")
logger.error("")
logger.fatal("")
```



force to rails don't log specific parameter by adding into config/application.rb

```ruby
config.filter_parameters += [:credit_card_number]
```


## test

rails has a minitest by default if you want use rspec it needs add

```ruby
group :development, :test do
  gem 'rspec-rails'
  # gem 'factory_girl_rails' # old fixture_replacement
  gem 'factory_bot_rails'
end

group :test do
  gem 'faker'
end
```

```bash
bundle install
bin/rails generate rspec:install
# to run the test

```




## authentication introduction

helper

model helper: has_secure_password
use blowfish require gem bcrypt installed, search into Gemfile
table must have a string column for password_digest


```ruby
#bin/rails generate migration AddPasswordDigestToModel

class < ActiveRecord::Migration(5.0)
  def up
    add_column "users", "password_digest", :string
  end
  def down
    remove_column "users", "password_digest", :string
  end
end

# bin/rails db:migrate

class Model
  has_secure_password

end
```

has_secure_password helper add
- attr_reader :password, with generate password_digest
- validates_presences_of :password, :on => :create
- validates_confirmation_of :password
- add method authenticate(unencrypted_password)


create a controller to access

```bash
bin/rails generate controller Access menu login

bin/rails generate controller namespace_name/controller_name
bin/rails generate controller api/v1/controller_name
```

```ruby
# add to routes
get 'access/menu'
get 'access/login'
post 'access/attempt_login'
get 'access/logout'
```


