# RAILS 6 - deployment in guebs

- a brief about server structure

we won't use the rails app as main app in the hosting
we use a `staging` as subdomain
we use as app name: `www-staging`
the app creation will create a `www-staging` folder
needs a folder to contain repo: `staging-repo`
needs a folder to contain capistrano folder: `staging`
needs replace a `www-staging` folder with link to `staging/current` release: www-staging
we need a `ruby/shared/staging` folder to contain production /config/database.yml to staging

the structure will be like as shown below

```

ls ~/ruby

repo-staging
staging
shared
www-staging-old
www-staging -> /home/${USER}/ruby/staging/current
```

- configure ssh


- configure subdomain into hosting

```
# subdomain staging
staging.${DOMAIN}.com 	
sites/staging.${DOMAIN}.com
/home/${USER}/sites/staging.${DOMAIN}
```

- configure new ruby app into hosting

```
# app: www-staging
staging.${DOMAIN}/
ruby/www-staging
/home/${USER}/ruby/www-staging

ruby 2.6
production
```


- configure repo into hosting using CLI

```
ssh -p 333 -i ~/.ssh/guebs_rsa ${USER}@${DOMAIN}

mkdir -p ~/ruby/shared
mkdir -p ~/ruby/shared/staging
mkdir -p ~/ruby/repo-staging
mkdir -p ~/ruby/staging
mkdir -p ~/ruby/staging/current
cd ~/ruby
mv www-staging www-staging-old
ln -s staging/current www-staging

cd ~/ruby/repo-staging
git init  --bare .
```



- configure remote into repo

```
git remote add  remote_name ssh://${USER}@${DOMAIN}:333/home/${USER}/ruby/repo-staging
```


- installation & config of capistrano into project

  + install gems into development group

```
group :development do
  gem "capistrano", "~> 3.11.2", require: false
  gem "capistrano-rails", "~> 1.4", require: false
  gem 'capistrano-dotenv', require: false
end
```  

  + configuration of capistrano

```
cap install

# src/Capfile
#-----------
	require "capistrano/setup"
	require "capistrano/deploy"
	require "capistrano/scm/git"
	install_plugin Capistrano::SCM::Git

	require 'capistrano/rails'
	require 'capistrano/bundler'
	require 'capistrano/dotenv'

	Dir.glob("lib/capistrano/tasks/*.rake").each { |r| import r }
#------------


# src/config/deploy.rb
#------------
	lock "~> 3.11.2"
	set :application, "staging"
	set :repo_url, "file:///home/${USER}/ruby/repo-staging"
	set :stages, ["production"]
	set :linked_files, %w{config/master.key}
	set :linked_files, %w{config/credentials.yml.enc}
#------------
# src/config/deploy/production.rb
#------------

#------------


# src/config/deploy/staging.rb
#------------
server '${DOMAIN}', user: '${USER}', roles: %w{app db web}, port: 333
set :tmp_dir, '/home/${USER}/tmp'
set :application, 'staging'
set :rails_env, :development
set :bundle_flags, '--quiet'
set :bundle_bins, %w(rake rails)
set :bundle_path, nil
after :deploy, 'deploy:restart'

set :repo_tree, 'src/'

set :repo_url, 'file:///home/${USER}/ruby/repo-staging'
set :deploy_to, '/home/${USER}/ruby/staging'
append :linked_files, "config/database.yml" 
#------------


# src/config/webpacker.yml
#     make sure that `webpack_compile_output: false`
```  

- create a task into `lib/capistrano/task`

```
# src/lib/capistrano/tasks/bundleinstall.rake
#------------
namespace :setup do
  desc 'Instala bundle en remoto'
  task :instala_bundle do
    on roles(:all) do
      execute 'gem install bundler'
    end
  end
end
# call on CLI `cap production setup:bundleinstall`
#------------

# src/lib/capistrano/tasks/bundleinstall.rake
#------------
namespace :deploy do
  desc 'restart aplication'
  task :restart do
    on roles(:all) do
      execute "touch #{current_path}/tmp/restart.txt"
    end
  end
end
# call on CLI `cap production deploy:restart`
#------------

```


- create .env-file into server vi `~/ruby/staging/shared/.env`

```
SECRET_KEY_BASE=wekja5w49ngaerj843taeij5s9iufmnzwe94m9qrztj
```

- add as linked files 

```ruby
# src/config/deploy.rb
set :linked_files, %w{.env} # DON'T WORK
```

FIX WITH BELOW (config/database should't exist in repo)

```
# src/config/deploy/staging
append :linked_files, "config/database.yml"
```

- node installation for webpacker use

+ A HACK: enable a subdomain as nodeapp to see the node executable to path location
+ see .bashrc

```
# User specific aliases and functions
PATH=$HOME/nodejs/testingnode/node_modules/.bin:$HOME/node_modules/yarn/bin:/opt/php7.0/bin:$HOME/ruby/gems/bin:/opt/git/bin:/opt/svn/bin:/opt/ruby-2.6/bin:/opt/nodejs-10/bin:$PATH:$HOME/bin
export PATH
```

/opt/nodejs-10/bin


```# User specific aliases and functions
PATH=/opt/nodejs-10/bin:$HOME/node_modules/yarn/bin:/opt/php7.0/bin:$HOME/ruby/gems/bin:/opt/git/bin:/opt/svn/bin:/opt/ruby-2.6/bin:$PATH:$HOME/bin
export PATH
```

```
npm install yarn
```

- settings the database configuration into hosting

first remove src/config/database.yml but preserving for local, and write into hosting

```
git rm --cached src/config/database.yml
echo config/database.yml >> .gitignore
git add .gitignore
git commit -m "removing database.yml to use capistrano"

ssh -p 333 -i ~/.ssh/guebs_rsa ${USER}@${DOMAIN}
vi ~/ruby/shared/staging/config/database.yml
```


- In rails 6 make sure that your app allow request for your hostname AKA domain

```
# config/environments/development.rb
config.hosts << "${SUBDOMAIN}.${DOMAIN}"
```


- ready to deploy


```
git push staging master

cd src # if use subfolder to capistrano files

cap staging deploy
cap production deploy
```

## when use `gem capistrano-rails`

```
cap {staging, production} deploy
cap {staging, production} deploy:migrate
cap {staging, production} deploy:compile_assets
```



# PROBLEMS




## when your project are into a subfolder like src


SSHKit::Runner::ExecuteError: Exception while executing as ${USER}@${DOMAIN}: bundle exit status: 10                                                                                                        
bundle stdout: Nothing written                                                                                                                                                                                     
bundle stderr: Could not locate Gemfile


```
# config/deploy/{staging,producion}.rb
set :repo_tree, 'src/'
```



## error: `Don't know how to build task 'assets:precompile'`

when you rails app don't have assets pipeline gem but Capistrano is searching, disable in capistrano this step


## error


```
00:07 deploy:assets:precompile
      01 bundle exec rake assets:precompile

ArgumentError: Missing `secret_key_base` for 'staging' environment, set this string with `rails credentials:edit`
```

EDITOR=vim rails credentials:edit

-> src/config/credentials.yml.enc
-> src/config/master.key


## problems

enable the develpment environment to show 