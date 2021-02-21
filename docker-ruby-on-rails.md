# how to docker an new rails app

notes:
if you use windows or cannot install rails into OS host, you can use rails into container
I have noted some problems with the routes in terminal emulator, maybe better use PowerShell



1. Structure creation

```bash
mkdir -p railsApp railsApp/src
cd railsApp
# search version of rails that you want install
# gem search rails --remote --all
```

2. Build Dockerfile

download images while, we will write Dockerfile

```bash
docker pull ruby:2.5.1 ; docker pull postgres:11.1
```

at railsApp/src

```Dockerfile
FROM ruby:2.5.1
LABEL MAINTAINER @stbnrivas
RUN \
  apt-get update && apt-get install -y \
  build-essential \
  libpq-dev \
  nodejs
RUN mkdir -p /app
WORKDIR /app
RUN gem install bundler && \
  gem install rails -v 5.2.2
RUN  rails new app / --database=postgresql \
  cd /app \
  bundle install --jobs 20 --retry 5 \
  gem install pg mysql2 sqlite3

EXPOSE 3000
# CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]
ENTRYPOINT /bin/bash # for generate rails app or to debug...
```

3. Build image

```bash
docker image build --tag rails:1.0 .
```

Obviously there a problem when you do that in windows:

SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. All files and directories added to build context will have '-rwxr-xr-x' permissions. It is recommended to double check and reset permissions for sensitive files and directories.

4. execute container from image to test

but when run container don't forget add volume to see app into src folder using mount sintax

```bash
docker run --interactive --tty --publish 3000:3000 --mount type=bind,source=$(pwd)/src,destination=/app rails:1.0
```

```powershell
docker run --interactive --tty --publish 3000:3000 --mount type=bind,source=${PWD}\\src,destination=/app rails:1.0
```

PROBLEM 

C:\Program Files\Docker\Docker\Resources\bin\docker.exe: Error response from daemon: driver failed programming external connectivity on endpoint thirsty_chaum (a4b3bb65ada07cdf304194d136aaacde29f572f5cd6a97e487e81b81ef1fead0): Error starting userland proxy: mkdir /port/tcp:0.0.0.0:3000:tcp:172.17.0.2:3000: input/output error.

Simply restart docker from systemtray


4.- Generate the rails project

inside the container 

```bash
pwd
rails new . --database=postgresql
exit
```

check into your host that rails project has been created

5. Reconfigure Dockerfile and build image again


```Dockerfile
FROM ruby:2.5.1
LABEL MAINTAINER @stbnrivas
RUN \
  apt-get update && apt-get install -y \ 
  build-essential \ 
  libpq-dev \
  nodejs
RUN mkdir -p /app 
WORKDIR /app
RUN gem install bundler && \
  gem install rails -v 5.2.2
RUN  rails new app / --database=postgresql \
  cd /app \
  bundle install --jobs 20 --retry 5
  gem install pg mysql2 sqlite3
EXPOSE 3000
CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]
# ENTRYPOINT /bin/bash # for generate rails app or to debug...
```


```bash
docker image build --tag rails:1.0 .
```


6. Run container from image with rails works


```bash
docker run --interactive --tty --publish 3000:3000 --mount type=bind,source=$(pwd)/src,destination=/app rails:1.0
```

```powershell
docker run --interactive --tty --publish 3000:3000 --mount type=bind,source=${PWD}\\src,destination=/app rails:1.0
```

7. Check in the browser to http://localhost:3000

could not connect to server: No such file or directory Is the server running locally and accepting connections on Unix domain socket "/var/run/postgresql/.s.PGSQL.5432"?

right this must be fail


if you have any problem right now you can use a terminal to the container

```bash
docker ps
# get container id 8f9f12aced43
docker container exec -it $container_id /bin/bash
bin/rails --help
```

you can exit with CTRL+C



8. Adding Postgresql to the equation... with docker-compose

this time we dont use Dockerfile, we will use docker-compose



```yml
version: '3'
services:
  postgres:
    image: "postgres:11.1"
    volumes:
    - ./db/development:/var/lib/postgresql/data
    ports:
      - "5432:5432"
  rails:
    build: .
    command: bundle exec rails server -p 3000 -b '0.0.0.0'
    volumes:
    - ./src:/app
    ports:
    - "3000:3000"
    depends_on:
    - postgres
```


9. set configuration to rails can connecto to postgresql

you need to find out the ip of network to connect rails with postgresql

```bash
docker network ls
docker network inspect bridge
# ... gateway  172.17.0.1 ...
```

at ./src/config/database.yml

```yml
default: &default
  adapter: postgresql
  encoding: unicode  
  #host: 172.17.0.1
  host: postgres
  username: postgres
  password:
  pool: 5

development:
  <<: *default
  database: myapp_development

# Warning: The database defined as "test" will be erased and
# re-generated from your development database when you run "rake".
# Do not set this db to the same as development or production.
test:
  <<: *default
  database: myapp_test
```


10. build images with docker compose


```bash
docker-compose build
# Successfully built b372a8469a71
# Successfully tagged railsapp_rails:latest
docker-compose up
```

you can check volumes with 

```bash
docker volume ls
```

also you can connect to postgres into terminal with

```bash
docker ps
# container id ac711deb75b3
docker exec --interactive --tty $CONTAINER_ID psql -h postgres -U postgres
docker exec --interactive --tty ac711deb75b3 psql -h postgres -U postgres
```


11. create database

by default at ./src/config/database.yml name is app_development

TODO: open pgsql

```sql
-- Database: app_development

-- DROP DATABASE app_development;

CREATE DATABASE app_development
    WITH
    OWNER = postgres
    ENCODING = 'UTF8'
    LC_COLLATE = 'en_US.utf8'
    LC_CTYPE = 'en_US.utf8'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1;
```



12. check directory to database has files

TODO: ./db/development/



13. the real work at rails begins


```bash
git init
git add .

```

add rubocop
```bash
rubocop --auto-gen-config
rubocop
```

docker creation
```bash
touch Dockerfile
touch docker.compose
touch .dockerignore
```




to get an terminal into container

```bash
docker ps
# get container id 8f9f12aced43
docker container exec -it $container_id /bin/bash
```




