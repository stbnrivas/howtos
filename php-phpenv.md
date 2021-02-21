# phpenv installation

```bash
sudo dnf install re2c curl lib-curl lib-curl-devel gcc-c++ libtidy libtidy-devel libzip libzip-devel
```


```bash
git clone git://github.com/phpenv/phpenv.git ~/.phpenv
echo 'export PATH="$HOME/.phpenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(phpenv init -)"' >> ~/.bash_profile

git clone https://github.com/php-build/php-build $(phpenv root)/plugins/php-build
```

## cli sintax

```bash
phpenv install 7.3.3
phpenv global 7.3.3
```


## composer, php dependences management

prerequirements:

```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

+ option 1 install global


+ option 2 intall locally into a project