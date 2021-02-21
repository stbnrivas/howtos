# creation of a gem


## a pure ruby gem

```bash
gem build  gem_name.gemspec
gem install ./gem_name.gem

bundle
```



## a ruby gem with c extension

https://dev.to/wataash/how-to-create-and-debug-ruby-gem-with-c-native-extension-3l8b


```
rbenv shell trunk # wtf is this?????
```

```bash
bundle gem example_ext --coc --ext --mit --test

# [--coc], [--no-coc] Generate a code of conduct file. Set a default with `bundle config set gem.coc true`.
# [--ext], [--no-ext] Generate the boilerplate for C extension code
# [--mit], [--no-mit] Generate an MIT license file. Set a default with `bundle config set gem.mit true`.
# [--test=rspec]
```