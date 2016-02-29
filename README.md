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
