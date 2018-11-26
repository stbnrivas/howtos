# workflow

write Dockerfile -> build image -> run container -> run bash into container -> 

```bash
  $ docker build --tag tag_name .
  $ docker tag 0e5574283393 fedora/httpd:version1.0
```
```bash
$ docker run --rm --interactive --tty --publish 80:80 --name --volume source:destination container_name image_name
```
```bash
docker run --rm --interactive --tty --publish 80:80 --name container_name image_name
```

## sinatraapp

```bash
$ mkdir src
$ touch src/app.rb src/Gemfile src/config.ru
```

```ruby
# Gemfile
source "https://rubygems.org"
git_source(:github) {|repo_name| "https://github.com/#{repo_name}" }
gem "sinatra"
gem "puma"
# config.ru
require File.expand_path('app', File.dirname(__FILE__))
run App
# app.rb
require 'sinatra/base'
class App < Sinatra::Application
  get '/' do
    'Put this in your pipe & smoke it!'
  end
end
```


## sinatra Dockerfile

```docker
FROM ruby:2.5.3
EXPOSE 9292/tcp
LABEL MAINTAINER stbnrivas

#ENV SRC="/src"

COPY src /src
RUN touch ~/.gemrc && echo "gem: --no-document" > ~/.gemrc

RUN apt-get update -qq \
  && apt-get install -y \
    build-essential \
    ruby-dev \
    bundler \
  && cd /src \
  && bundler install

WORKDIR /src
CMD ["bundle","exec","rackup","--host","0.0.0.0","-p","9292"]
```



## clean container stuff if explotation?

```docker
RUN ...
  && apt-get clean autoclean \
  && apt-get autoremove -y \
  && rm -rf \
    /var/lib/apt \
    /var/lib/dpkg \
    /var/lib/cache \
    /var/lib/log
```