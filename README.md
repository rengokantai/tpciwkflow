#### tpciwkflow

- 2  
create `.travis.yml`  
edit:
```
language: ruby
rvm:
  - 2.1.0
  - 2.2.0
addons:
  postgresql: "9.4"
before_script:
  - psql -c 'create database test;' -U postgres
  - cp config/database.yml.travis config/database.yml
```
create `database.yml.travis`
```
test:
  adapter: postgresql
  database: test
  username: postgres
```

some RSpec syntax
```
get :index
expect(assigns(:authors).count).to eq(Author.count)
get :index
expect(response).to render_template(:index)
get :new
expect(assigns(:author)).to be_a_new(Author)
get :new
expect(response).to render_template(:new)
```


#### engine yard

- 3
######Codeship
create a ruby proj, then
```
bundle exec rake spec:models
bundle exec rake spec:controllers
bundle exec rspec
buncle exec cucumber
```

syntax review:
```
rails g rspec:controller publishers
```
######Heroku
```
heroku login
heroku create
heroku addons:create heroku-postgresql:hobby-dev

heroku apps  #get app name
heroku run rake db:seed
```
- 4  
######Jenkins:  
configure global secu->Jenkins own user database(allow users to sign up)  
Auth->matrix-based secu(add your username)(select all ticks)  
prevent csrf exploit  

  
install github and git client plugin.  
resetart jenkins when installations is complete and no jobs are running.  
for ruby, install rvm and rake plugin.  


build a new freestyle project.  
enter github project link, SCM->Git, Repo url(same as above)  
install tools in CI server:
```
apt-get install build-essential git-core curl postgresql libpq-dev
```
install rvm.  
buildenv->run the build in rvm(ruby@rengokantai)  
then execute shell `gem install bundler --no-ri --no-doc`
invoke rake  

######test ruby
install plugins: rubymetrics plugin, xunit  
set add*build when a change is pushed to github

ADD a script:`export RAILS_ENV=test`
ADD a invoke rake:
```
db:create
db:schema:load
```
Another rake:
```
spec SPEC_OPTS="--format RSpecJunitFormatter --out rspec.xml"
```
add post-build action:  
publish rcov report
publish xunit(add junit pattern)  

in postgres, create a new user:
```
su - postgres
createuser -s jenkins
```

add three gems:
```
gem 'simplecov'
gem 'simplecov-rcov'
gem 'rspec_junit_formatter'
```
and add to rails_helper.rb

go to github->webhooks->add Jenkinsgithub, add link: http://jenkins/github-webhook  


run config/database.yml
```
production:
  adapter: postgresql
  encoding: unicode
  pool: 5
  database: production
```

then
```
cap production deploy
```
