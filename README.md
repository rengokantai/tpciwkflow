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
- 4  
Jenkins:  
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



