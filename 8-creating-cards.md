## 5 - Creating Profiles

### Generate model and controller for profile

For profile this are the fields created for the moment:

```ruby
nickname:string
phone:string
email:string 
is_solidarity:boolean
is_published:boolean
subdomain:string    
domain:string
```

**terminal**

    rails generate model card nickname:string phone:string email:string is_solidarity:boolean is_published:boolean subdomain:string domain:string

    rails g scaffold_controller Card

set relation user and profile (in db)

**db/migrate/____create_profiles**

```ruby
t.belongs_to :user, index: true
```
set relation user and profile and valitations (in models), can be has_one or has_many

**app/models/user.rb**

```ruby
has_many :profile
```

**app/models/card.rb**

```ruby
belongs_to :user
```

```ruby
validates :name, presence: true
validates :description, presence: true
validates :user, presence: true
```
**config/routes.rb**  

```ruby
resources :profiles
```

**app/controllers/card_controller.rb**

find:

```ruby
  def profile_params
    params[:profile]
  end
```

And change for:

```ruby
  def profile_params
    params.require(:profile).permit(
      nickname:string
      phone:string
      email:string 
      is_solidarity:boolean
      is_published;.boolean
      subdomain:string    
      domain:string
    )
  end
```

**spec/controllers/profile_controller_spec.rb**

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