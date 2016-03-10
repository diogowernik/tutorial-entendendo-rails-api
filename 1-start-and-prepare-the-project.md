## 1 - Start and Prepare the project.

Install gem rails-api

    gem install rails-api


Create rails-api

    rails-api new simple-api
    
Delete test folder, because we are going to use rspec for tests

**Gemfile**

Edit gem file, installing gems for the api:


```ruby
    gem 'devise_token_auth'

    gem 'omniauth'

    group :development, :test do
      gem 'rspec-rails', '~> 3.0'
      gem 'rubocop', '~> 0.37.2', require: false
    end
```

On teminal

    bundle install
    rake db:migrate

Insert .rubocop.yml in the project root

```ruby
# This is the configuration used to check the rubocop source code.
# Check out: https://github.com/bbatsov/rubocop

AllCops:
  Include:
    - '**/Rakefile'
    - '**/config.ru'
  Exclude:
    - 'vendor/**/*'
    - 'spec/fixtures/**/*'
    - 'db/**/*'
    - 'db/schema.rb'
    - 'db/seeds.rb'
    - 'client/node_modules/**/*'
    - 'bin/**/*'
    - 'config/initializers/secret_token.rb'
    - !ruby/regexp /old_and_unused\.rb$/
    
Metrics/LineLength:
  Max: 120
  
Style/Documentation:
  Enabled: false

Style/BlockDelimiters:
  Enabled: false

Style/StringLiterals:
  Enabled: false
  
Style/SymbolArray:
  Enabled: false
```

Gerar rpec 

    rails generate rspec:install

Test all

    rspec
    rubocop

First Commit with git

    git init
    git add -A .
    git commit -m "Project Start"