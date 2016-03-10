## 5 - Creating Publications

### Generate model and controller for publications

For publication this are the fields created for the moment:

```ruby
title:string
description:text
type:string
is_published:boolean
```

**terminal**

    rails generate model publication title:string description:text type:string is_published:boolean

    rails g scaffold_controller Publication

set relation profile and publications (in db)

**db/migrate/____create_publications**

```ruby
t.belongs_to :profile, index: true
```
set relation publication and profile and valitations (in models), can be has_one or has_many

**app/models/profile.rb**

```ruby
has_many :publication
```

**app/models/publication.rb**

```ruby
belongs_to :profile
```

```ruby
validates :title, presence: true
validates :description, presence: true
validates :type, presence: true
validates :profile, presence: true
```
**config/routes.rb**  

```ruby
resources :publications
```

**app/controllers/publication_controller.rb**

And change the def set params:

find:

```ruby
  def publication_params
    params[:publication]
  end
```
And change for:  

```ruby
  def publication_params
    params.require(:publication).permit(
      :title,
      :description,
      :type,
      :profile_id
    )
  end
```



**spec/controllers/publication_controller_spec.rb**

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