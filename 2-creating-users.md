## 2 - Creating Users

### Create Model for users using devise token auth


    rails g devise_token_auth:install User auth


**db/migrate/___create_users.db**

on line 37, delete:

```ruby
t.string :name
t.string :nickname
t.string :image
```

Install the migrate generated

    rake db:migrate

In the folder:

**app/model/user.rb** 

align the paramters and for tests comment the confirmable config.
(so we dont need to confirm email for tests at this moment)

```ruby
# , :confirmable
```

### Create controllers for users

    rails g scaffold_controller User

**app/controller/users_controller.rb**

- add that for authentication:

```ruby
before_action :authenticate_user!, except: [:show, :index]
```

- delete post, that will be managed from devise_token_auth

```ruby
  # POST /users
  # POST /users.json
  def create
    @user = User.new(user_params)
    if @user.save
      render json: @user, status: :created, location: @user
    else
      render json: @user.errors, status: :unprocessable_entity
    end
  end
```

- change the def user_params, last lines

```ruby
def user_params
params.require(:user).permit(:email)
end
```

### Set the routes

**config/routes.rb**

```ruby
resources :users
```