- Para api authenticação baseado em token

Adicionar as gems:

    gem 'devise_token_auth'
    gem 'omniauth'

Criar users auth

    rails g devise_token_auth:install User auth

Deletar banco de dados e gerar outro novo.

    rake db:drop && rake db:create && rake db:migrate

Criar controller

    rails g scaffold_controller User

inserir em app/controller/users_controller.rb

    before_action :authenticate_user!, :except => [:show, :index]
    
- Ferramenta para analise de codigo

  Estatica ou Execução

    gem 'rubocop', '~> 0.37.2', require: false
 
 Inserir arquivo .rubocop.yml na raiz do projeto