docker-rails-stub
===
Very simple set of files to help bootstrap a rails app in docker using postgres so that the docker evironment doesn't need to be installed on you machine -- eliminating conflicting version management and other nasties.

This repository is optimized for working on a Windows OS. Adapted from docker.com instructions [here](https://docs.docker.com/compose/rails/)

## Getting started
Make sure that you have `docker` and `docker-compose` installed on your machine.

### 
clone into directory name of your choice `git clone https://github.com/beartums/docker-rails-stub.git <directoryname>`. CD to that directory and build:
```
docker-compose build
```

Create your application with:
```
docker-compose run web rails new . --force --no-deps --database=postgresql
```
This should populate your folder with all the files needed to run a rails app.  We're almost there!

Edit your gemfile and replace `gem 'sass-rails', '~> 5.0'` with `gem 'sassc-rails'`

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

Browse to localhost:3000.  You should see the rails place holder.  YAY!

NOTE:
1. If you make any changes to the gemfile, you will need to run `docker-compose build` or `docker-compose up --build`
for your installation to save the changes

2. You can add dependencies using yarn, but only in a running container.
Once you have the container running (`docker-compose up`) open another
terminal in the same folder and run `docker exec -it <folder>_web_1 /bin/bash`
to open a terminal in the running container.  you can run yarn from this command line
, as well as rails c, or any other command you need to run for debugging and
development

## Useful commands:
<dl>
      <dt>docker-compose stop</dt>
      <dd>Stop the running containers</dd>
      <dt>docker-compose down</dt>
      <dd>Stop and remove the running containers</dd>
      <dt>docker-compose up --build</dt>
      <dd>Build the containers before starting them</dd>
      <dt>docker-compose run web bundle install</dt>
      <dd>Run the gem bundler.  (replace `bundle install` with any other one-off command)
      <dt>*docker exec -it &lt;folderName&gt;_web_1 /bin/bash*</dt>
      <dd>Open a bash prompt in the container hosting the server.  This is probably the most 
      important command.  From here you can run any useful commands in the rails environment, 
      like `rails console`, `yarn install --check-files`, `yarn add ...` etc.  You *must*
      update your rails environment here, rather than at your windows terminal</dd>
</dl>

### Add React
more to come...
<!-- add webpacker and react-rails to gemfile
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
    <-- Following will make the react components availabe to our layout --
    %= javascript_pack_tag 'application' %
	
create home/index.erb:
	<%= react_component 'GreetUser', name: 'Ankur' %>
	
Use styles
???add to gemfile: gem 'bootstrap'
yarn add bootstrap popper.js jquery npm

npm rebuild node-sass

docker-compose build
import './src/application' -> app/javascript/packs/application.js
import 'bootstrap' -> ditto
into app/javascript/packs/src/application.scss
	@import '~bootstrap/dist/css/bootstrap';
	@import './custom.scss';
	
docker-compose run web yarn install --check-files -->
