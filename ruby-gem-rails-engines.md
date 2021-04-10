# rails engine

A rails engine it's a Rails App which run into a Rails App

some gem are rails plugins
some rails plugins are rails engines

Why write a rails engine?
- you need a library/gem reusable across multiple rails app
- your monolith is a monster and you need to cut it up into smaller pieces




```bash
mkdir -p rails-root-app/engines
cd rails-root-app/engines

rails plugin new subapp --mountable
```

```ruby
# config/routes.rb

mount SubApp::Engine => "subapp_path"
```

```ruby
# Gemfile of rails-root-app

gem "subapp", path: "engines/subapp"
```


