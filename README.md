#### tpciwkflow

- 2  
create `travis.yml`  
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
  
