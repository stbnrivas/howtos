# some gems and spices for sinatra

    gem install shotgun, racksh

- shotgun reload app without restart the server

    shotgun app.rb
    shotgun config.ru

- you can use irb or racksh is like rails console for sinatra

    irb -r app.rb
    bundle exec irb -r app.rb

OR

    gem racksh

 To start racksh session run following inside rack application directory (containing config.ru file):

 
