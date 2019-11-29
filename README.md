clone into directory name of your choice
#edit docker-compose.yml to set your app name
create app: docker-compose run web rails new . --force --no-deps --database=postgresql
replace rails-sass with sassc in gemfile
docker-compose build
update config/database.yml with db.yml.example
docker-compose up
docker-compose run web rake db:create
browse to localhost:3001

useful commands:
docker-compose stop
docker-compose down
docker-compose up --build
docker-compose run web bundle install
docker-compose exec -it rails_web_1 /bin/bash

add react
add webpacker and react-rails to gemfile
add this to dockerfile:  && \
      curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
      echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
      apt-get update && apt-get install -y yarn
	  
	  Also: "&& yarn install --check-files" after bundle install
$ docker-compose build

$ docker-compose run web rails webpacker:install
$ docker-compose run web rails webpacker:install:react
$ docker-compose run web rails generate react:install

add to app/views/layouts/application.html.erb (in <head>:
    <!-- Following will make the react components availabe to our layout -->
    <%= javascript_pack_tag 'application' %>
	
create home/index.erb:
	<%= react_component 'GreetUser', name: 'Ankur' %>
	
Use styles
???add to gemfile: gem 'bootstrap'
yarn add bootstrap
yarn add popper
yarn add jquery

docker-compose build
import './src/application' -> app/javascript/packs/application.js
import 'bootstrap' -> ditto
into app/javascript/packs/src/application.scss
	@import '~bootstrap/dist/css/bootstrap';
	@import './custom.scss';
	
docker-compose run web yarn install --check-files
