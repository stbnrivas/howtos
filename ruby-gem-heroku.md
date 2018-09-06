# heroku gem

		gem install heroku
		heroku login
		heroku create
		git remote add heroku

# deploy

		heroku create
		git push heroku master
		heroku run rake db:migrate
		heroku open

# heroku docker

		heroku plugins:install heroku-docker
		heroku docker:init
		docker compose run shell
		bundle exec rake db:migrate
