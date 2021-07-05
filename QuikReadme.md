
### Basic Rails setup instructions for Docker

```
* Create Gemfile with following instructions

source 'https://rubygems.org'
gem 'rails', '6.1.3'

* Create empty Gemfile.lock file

* Create docker-compose.yml and Dockerfile

$ docker-compose run app rails new . --force --database=mysql --skip-bundle

* Change database settings in /config/database.yml

default: &default
  adapter: mysql2
  encoding: utf8
  pool: 5
  database: <%= ENV['DB_NAME'] %>
  username: <%= ENV['DB_USER'] %>
  password: <%= ENV['DB_PASSWORD'] %>
  host: <%= ENV['DB_HOST'] %>

development:
  <<: *default

test:
  <<: *default

production:
  <<: *default


$ docker-compose run --rm app bundle exec rake webpacker:install
$ docker-compose build
$ docker-compose up (to start the docker build)
$ sudo docker exec -it rails-quikposts_app_1 /bin/sh (to execute rails commands in container)
```