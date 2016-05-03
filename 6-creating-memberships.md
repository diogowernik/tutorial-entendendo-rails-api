## 5 - Creating Publications

### Generate model and controller for publications

For publication this are the fields created for the moment:

```ruby
plan:string
start_date:date
finish_date:date
is_active:boolean
price:interger
access_level:string
trial_active:boolean
trial_duration:interger
payment_methods:string
recurring_subscription:boolean
recurring_payments:integer
```

**terminal**

    rails generate model membership plan:string start_date:date finish_date:date is_active:boolean price:interger access_level:string trial_active:boolean trial_duration:interger payment_methods:string recurring_subscription:boolean recurring_payments:integer

    rails g scaffold_controller Membership

set relation membership and user (in db)

**db/migrate/____create_membership**

```ruby
t.belongs_to :user, index: true
```

**app/models/user.rb**

```ruby
has_one :membership
```

**app/models/publication.rb**

```ruby
  belongs_to :user
  validates :plan, presence: true
  validates :start_date, presence: true
  validates :finish_date, presence: true
  validates :user, presence: true
  validates :price, presence: true
  validates :access_level, presence: true
```
**config/routes.rb**  

```ruby
resources :memberships
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
      :plan,
      :start_date,
      :finish_date,
      :is_active,
      :price,
      :access_level,
      :trial_active,
      :trial_duration,
      :payment_methods,
      :recurring_subscription,
      :recurring_payments
    )
  end
```

**spec/controllers/membership_controller_spec.rb**

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

    git checkout -b feature/publications_controller
    git add -A .
    git commit -m "publications created"
    git push origin feature/publications_controller