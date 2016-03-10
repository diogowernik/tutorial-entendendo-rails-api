Deletar banco de dados e gerar outro novo.

    rake db:drop && rake db:create && rake db:migrate

need to delete models

    rails destroy model profile
    
need to delete db data

    rails c
    Profile.delete_all

When working on validation models:

    boolean do not use validate

check the codewith rubocop 

    rubocop

Update your entire project to Ruby 1.9 hash syntax

http://effectif.com/ruby/update-your-project-for-ruby-19-hash-syntax

    find . -name \*.rb -exec perl -p -i -e 's/([^:]):(\w+)\s*=>/\1\2:/g' {} \;

    rubocop
    
and manually correct what it sugests