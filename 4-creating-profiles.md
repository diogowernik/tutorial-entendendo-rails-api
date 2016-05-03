## 5 - Creating Profiles

### Generate model and controller for profile

For profile this are the fields created for the moment:

```ruby
name:string
image:string
description:text
site_url:string
blog_url:string
phone:string
mobile_phone:string
google_plus:string 
facebook_page:string
instagram:string 
twitter:string
tags:string
```

**terminal**

    rails generate model profile name:string image:string description:text site_url:string blog_url:string phone:string mobile_phone:string google_plus:string facebook_page:string instagram:string twitter:string tags:string

    rails g scaffold_controller Profile

set relation user and profile (in db)

**db/migrate/____create_profiles**

```ruby
t.belongs_to :user, index: true
t.belongs_to :card, index: true
```
set relation user and profile and valitations (in models), can be has_one or has_many

**app/models/user.rb**

```ruby
has_many :profile
```

**app/models/card.rb**

```ruby
has_one :profile
```

**app/models/profile.rb**

```ruby
belongs_to :user
belongs_to :card
validates :name, presence: true
validates :description, presence: true
validates :user, presence: true
validates :card, presence: true
```
**config/routes.rb**  

```ruby
resources :profiles
```

**app/controllers/profile_controller.rb**

find:

```ruby
def profile_params
    params.require(:profile).permit(
      :name,
      :image,
      :description,
      :site_url,
      :blog_url,
      :phone,
      :mobile_phone,
      :google_plus, 
      :facebook_page,
      :instagram,
      :twitter,
      :tags,
      :user_id,
      :card_id
    )
  end
```

And change for:

```ruby
  def profile_params
    params.require(:profile).permit(
      :name,
      :description,
      :user_id
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
    rubocop

git on all

    git checkout -b feature/profiles_controller
    git add -A .
    git commit -m "profiles created"