## 8 - Creating Cards

### Generate model and controller for card

For card this are the fields created for the moment:

```ruby
name:string
image:string
phone:string
email:string 
subdomain:string
domain:string
tags:string
is_solidarity:boolean
is_published:boolean
```

**terminal**

    rails generate model card name:string image:string phone:string email:string subdomain:string domain:string tags:string is_solidarity:boolean is_published:boolean

    rails g scaffold_controller Card

set relation user and card (in db)

**db/migrate/____create_cards**

```ruby
t.belongs_to :user, index: true
```
set relation user and profile and valitations (in models), can be has_one or has_many

**app/models/user.rb**

```ruby
has_many :card
```

**app/models/card.rb**

```ruby
  belongs_to :user
  validates :name, presence: true
  validates :domain, presence: true
  validates :subdomain, presence: true
  validates :user, presence: true
```
**config/routes.rb**  

```ruby
resources :cards
```

**app/controllers/card_controller.rb**

find:

```ruby
  def profile_params
    params[:card]
  end
```

And change for:

```ruby
  def card_params
    params.require(:card).permit(
      :name.
      :phone,
      :email,
      :subdomain,
      :domain,
      :tags,
      :is_solidarity,
      :is_published
    )
  end
```

**spec/controllers/card_controller_spec.rb**

delete because is for rails full application, not needed for only rails-api:

```ruby
describe "GET #new" do
(...)
end

describe "GET #edit" do
(...)
end

it "redirects to the created ..." do
(...)
end
  
it "re-renders the 'new' template" do
(...)
end

it "re-renders the 'edit' template" do
(...)
end
```

db install:

    rake db:migrate

Run rspec to check the app

    rspec

Git new branch:

    git checkout -b feature/cards_controller
    git add -A .
    git commit -m "card created"