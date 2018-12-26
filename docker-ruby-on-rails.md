# how to docker an new rails app

structure creation 

```bash
mkdir -p rails-with-docker
rails new src
git init
git add .
git commit -m "rails new src"
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

```Dockerfile
FROM ruby:2.5.1
LABEL MAINTAINER @stbnrivas

RUN \
  apt-get update && apt-get install -y \ 
  build-essential \ 
  nodejs
RUN mkdir -p /app 
WORKDIR /app
COPY ./src/Gemfile ./src/Gemfile.lock ./ 
RUN gem install bundler && bundle install --jobs 20 --retry 5
COPY src ./
EXPOSE 3000
CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]
```



```bash
docker build --tag rails-demo .
```

test if test run container from image 

```bash
docker run --interactive --tty --rm rails-demo bundle exec rake test
```

execute rails 
```bash
docker run --interactive --tty --publish 3000:3000 rails-demo
```

execute rails with volume 
```bash
docker run --interactive --tty --publish 3000:3000 --volume ./src:/app rails-demo
```

execute rails with volume using mount sintax
```bash
docker run --interactive --tty --publish 3000:3000 --mount type=bind,source=./src,destination=/app rails-demo
```

```powershell
docker run --interactive --tty --publish 3000:3000 --mount type=bind,source=${PWD}/src,destination=/app rails-demo
```

to get an terminal into container

```bash
docker ps
# get container id 8f9f12aced43
docker container exec -it $container_id /bin/bash
```




using docker-compose to set database postgresql

```docker-compose
app:
  build: .
  command: rails server -p 3000 -b '0.0.0.0'
  # command: rails server --port 3000 --binding=0.0.0.0
  # command: bundle exec rails server -p 3000 -b '0.0.0.0'
  volumes:
    - ./src:/app
  ports:
    - "3000:3000"
```

```bash
docker-compose build
docker-compose up
```


adding PostgreSQL

```docker-compose
app:
  build: .
  command: rails server -p 3000 -b '0.0.0.0'
  volumes:
    - .:/app
  ports:
    - "3000:3000"
  links:
    - postgres
postgres:
  image: postgres:9.4
  ports:
    - "5432"
```


# replicate environment into another machine