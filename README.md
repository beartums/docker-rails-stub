docker-rails-stub
===
Very simple set of files to help bootstrap a rails app in docker using postgres so that the docker evironment doesn't need to be installed on you machine -- eliminating conflicting version management and other nasties.

This repository is optimized for working on a Windows OS. Adapted from docker.com instructions [here](https://docs.docker.com/compose/rails/)

## Getting started
Make sure that you have `docker` and `docker-compose` installed on your machine.

### 
clone into directory name of your choice.  Now run
```
docker-compose build
```

Create your application with:
```
docker-compose run web rails new . --force --no-deps --database=postgresql
```
This should populate your folder with all the files needed to run a rails app.  We're almost there!

Edit your gemfile and replace `rails-sass` with `sassc`

run 
```
docker-compose build
```

Now you need to edit the `config/database.yml` file to be able to connect to the 
database. Copy the uncommented lines from `/db.yml.example`

create the database for rails with
```
docker-compose run web rake db:create
```

start the server: `docker-compose up`

browse to localhost:3001

####Useful commands:
<dl>
<dt>docker-compose stop</dt>
<dd>Stop the running containers</dd>
<dt>docker-compose down</dt>
<dd>Stop and remove the running containers</dd>
<dt>docker-compose up --build</dt>
<dd>Build the containers before starting them</dd>
<dt>docker-compose run web bundle install</dt>
<dd>Run the gem bundler.  (replace `bundle install` with any other one-off command)
<dt>docker-compose exec -it rails_web_1 /bin/bash</dt>
<dd>open a bash prompt in the container hosting the server.  From here you can run any useful commands, like `rails console`,
`yarn install --check-files`, `ran add ...` etc</dd>
</dl>

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
yarn add popper.js
yarn add jquery

docker-compose build
import './src/application' -> app/javascript/packs/application.js
import 'bootstrap' -> ditto
into app/javascript/packs/src/application.scss
	@import '~bootstrap/dist/css/bootstrap';
	@import './custom.scss';
	
docker-compose run web yarn install --check-files
