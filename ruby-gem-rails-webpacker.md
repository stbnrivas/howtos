# webpacker

```
bin/rails webpacker:install:react
```

```ruby
# DONT USE javascript_include_tag() it is for assets pipeline

javascript_pack_tag('file_at/app/javascript/packs') # for js files using webpacker
```



<%= javascript_pack_tag("hello_react") %>