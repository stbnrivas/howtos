
# installation and use of ruby with rbenv

ruby need some package dependences to install natively some extensions because it need recompile

```bash
dnf groupinstall "Development Tools"

dnf install libsq3.x86_64
dnf install sqlite3-devel ruby-sqlite3 libsqlite3x-devel libsqlite3x
dnf install -y libxml2 libxml2-devel libxslt libxslt-devel
dnf install -y nokogiri
dnf install -y openssl-devel readline-devel
```

## PROBLEM IN FEDORA 29

MAY BE YOU MUST REPLACE ALL CONFIG AT ~/.bash_profile to ~/.bashrc
because  you can't do  source ~/.bash_profile into ~/.bashrc or terminal won't start

## rbenv install

```bash
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
```
type rbenv to test

## rbenv plugin: The ruby-build plugin provides an rbenv install uninstall command

```bash
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
```

## for rbenv rehash automatically after install or any command

- Option 1: rbenv plugin
```bash
git clone https://github.com/sstephenson/rbenv-gem-rehash.git ~/.rbenv/plugins/rbenv-gem-rehash
```

- Option 2: rbenv rehash with adding ~/.bash_profile
```bash
export PATH="$HOME/.rbenv/bin:$PATH"
export PATH="/home/stbn/.rbenv/shims:${PATH}"
export RBENV_SHELL=bash
source '/home/stbn/.rbenv/libexec/../completions/rbenv.bash'
command rbenv rehash 2>/dev/null
rbenv() {
  local command
  command="$1"
  if [ "$#" -gt 0 ]; then
    shift
  fi

  case "$command" in
  rehash|shell)
    eval "$(rbenv "sh-$command" "$@")";;
  *)
    command rbenv "$command" "$@";;
  esac
}
```

## rbenv plugin: rbenv-gemset is an extension for the rbenv ruby version manager that allows you to use "gemsets", sandboxed collections of gems. This lets you have multiple collections of gems installed in different sandboxes, and specify

```bash
git clone git://github.com/jf/rbenv-gemset.git $HOME/.rbenv/plugins/rbenv-gemset
```





# update and installation of rbenv

```bash
cd ~/.rbenv
git pull
```

# rbenv commands

Displays the full path to the binary that rbenv will execute when you run the given command

```bash
  gem environment
```

installations of diferents ruby versions

```bash
rbenv install -l
rbenv install --list

rbenv install 1.8.7-p375
rbenv install 2.1.2

rbenv uninstall ruby-1.8.7-p358

rbenv rehash                          even you do gem install gem must run this command

rbenv global 1.8.7-p375               set to global default version
rbenv global				                  check global version

cd project-dir                        
rbenv local 1.8.7-p375                set to project dir to ruby version by .rbenv dir
rbenv local                           check local directory version


rbenv -v                                version of rbenv
rbenv version                           display the currently active version of ruby
rbenv versions                          display all the currently installed versions of ruby

rbenv whence <gem>                      return list all Ruby versions that contain the given executable

#  example: rbenv whence rackup
#    1.9.3-p551

rbenv which <gem> # Displays the full path to the executable that rbenv will invoke when you run the given command.

#  example: rbenv which irb
#    /usr/bin/irb

rbenv exec gem install bundler


echo 'gem: --no-ri --no-rdoc' >> ~/.gemrc # that is for not install ri and rdoc
```




## launch shell of specific ruby version

```bash
rbenv shell 1.8.7-p375
rbenv shell --unset
```

## installing gem in a specific ruby version

```bash
rbenv shell 2.0.0-p247
gem install bundler  # bundler is installed for Ruby 2.0.0-p247 only
rbenv rehash # to set visible
rbenv shell 1.9.3-p447
gem install bundler
```


# PLUGIN: gemset (installation yours gem into project folder )

```bash
  git clone git://github.com/jf/rbenv-gemset.git $HOME/.rbenv/plugins/rbenv-gemset
```

## example

```bash
rbenv gemset # show the help

# first create the gemset for a specific version of ruby and give it a name
rbenv gemset create [ruby_version] [gemset_name]
rbenv gemset create 2.5.3 $gs_for_project_name
# move to the project folder
cd project
# set gemset to the project
rbenv gemset init [gemset_name]
rbenv gemset init $gs_for_project_name
# it will create a file .rbenv-gemsets
# ...
rbenv gemset list
rbenv gemset delete $gs_for_project_name
```







# Now let's put all together into a new project

```bash
mkdir Developer
rbenv version # if there some version installed
rbenv install -l # if we want search a version to install
```

sometimes when problem arise better way is update rbenv and plugins

```bash
cd ~/.rbenv/
cd ~/.rbenv/plugins/ruby-build; git pull
cd ~/.rbenv/plugins/rbenv-gemset; git pull
```

select your ruby version and install

```bash
rbenv install 2.5.1
```

set this version locally into folder or global

```bash
rbenv global 2.5.1
rbenv local 2.5.1
```

install gems

```bash
  gem uninstall -all # from start clean space
  gem install rails --version=5.1 --no-rdoc --no-ri
```

create new project

```bash
rails new depot; cd depot
rbenv local 2.5.1
rbenv gemset create 2.5.1 gemset-rails-5.1
rbenv gemset init gemset-rails-5.1
```

you can manage with this

```bash
rbenv gemset list
rbenv gemset delete [version] [gemset]
```

rbenv-doctor

curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash




# the old old way: installation of ruby versions manually

get versions manually of https://ftp.ruby-lang.org/pub/ruby/

```bash
wget https://ftp.ruby-lang.org/pub/ruby/ruby-1.8.7-p358.tar.gz -P $HOME/.rbenv/versions/
tar xvfz ruby-1.8.7-p358.tar.gz

./configure --prefix=/home/stbn/.rbenv/versions/ruby-1.8.7-p358
./configure --prefix=$HOME/.rbenv/versions/1.9.2-p290

rbenv rehash

make
make install
```
