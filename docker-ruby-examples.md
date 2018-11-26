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

```Dockerfile
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

```Dockerfile
RUN ...
  && apt-get clean autoclean \
  && apt-get autoremove -y \
  && rm -rf \
    /var/lib/apt \
    /var/lib/dpkg \
    /var/lib/cache \
    /var/lib/log
```

#



# Development with docker: mounting volumes

Instead, store data with COPY you must use bind mounts to give your container access to your source code. 

## workflow:
- build container only with COPY Gemfile to /gems 
- create a volume with source code  
- run container mounting volume with source code


```bash
$ docker volume create my-vol
$ docker volume inspect my-vol
$ docker volume rm my-vol
```

execute a container with a docker volume

```bash
$ docker run -d \
  --name devtest \
  --mount source=myvol2,target=/app \
  nginx:latest
```


```Dockerfile
FROM ruby:2.5.3
EXPOSE 9292/tcp
LABEL MAINTAINER stbnrivas

#ENV SRC="/src"

COPY src/Gemfile /src-dependences
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



```Dockerfile
FROM ruby:2.4.0
RUN apt-get update
RUN apt-get install -y build-essential nodejs imagemagick
# Point Bundler at /gems. This will cause Bundler to re-use gems that have already been installed on the gems volume
ENV BUNDLE_PATH /gems
ENV BUNDLE_HOME /gems 
# Increase how many threads Bundler uses when installing. Optional!
ENV BUNDLE_JOBS 4 
# How many times Bundler will retry a gem download. Optional!
ENV BUNDLE_RETRY 3 
# Where Rubygems will look for gems, similar to BUNDLE_ equivalents.
ENV GEM_HOME /gems
ENV GEM_PATH /gems 
# You'll need something here. For development, you don't need anything super secret.
ENV SECRET_KEY_BASE development123 
# Add /gems/bin to the path so any installed gem binaries are runnable from bash.
ENV PATH /gems/bin:$PATH RUN gem install bundler
# Allow SSH keys to be mounted (optional, but nice if you use SSH authentication for git)
VOLUME /root/.ssh 
# Setup the directory where we will mount the codebase from the hostVOLUME /appWORKDIR /app 
CMD /bin/bash

This Dockerfile is a good base for developing Rails application
```