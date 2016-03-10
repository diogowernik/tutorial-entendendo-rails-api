## Test Users 

### Test Manually

Install Postman

got to:

yoursite.com/auth

Insert the data and see te return

### Automated tests

Rspec

**spec/controllers/users_controller_spec.rb**

```ruby

require 'rails_helper'

RSpec.describe UsersController, type: :controller do
  let(:valid_attributes) {
    { email: 'batman@gothan.io', password: 'Senha1234' }
  }
  let(:invalid_attributes) {
    { user: {} }
  }
  let(:valid_session) { {} }
  describe 'GET #index' do
    it 'assigns all users as @users' do
      user = User.create! valid_attributes
      get :index, {}, valid_session
      expect(assigns(:users)).to eq([user])
    end
  end
  describe 'GET #show' do
    it 'assigns the requested user as @user' do
      user = User.create! valid_attributes
      get :show, { id: user.to_param }, valid_session
      expect(assigns(:user)).to eq(user)
    end
  end
  describe 'PUT #update' do
    context 'with valid params' do
      let(:new_attributes) {
        { email: 'bruce@gothan.io' }
      }
      it 'updates the requested user' do
        skip
        user = User.create! valid_attributes
        put :update, { id: user.to_param, user: new_attributes }, valid_session
        user.reload
        expect(user.email).to eql(new_attributes[:email])
      end
      it 'assigns the requested user as @user' do
        user = User.create! valid_attributes
        val_params = { id: user.to_param, user: valid_attributes }
        put :update, val_params, valid_session
        expect(assigns(:user)).to eq(user)
      end
      it 'redirects to the user' do
        skip
        user = User.create! valid_attributes
        val_params = { id: user.to_param, user: valid_attributes }
        put :update, val_params, valid_session
        expect(response).to redirect_to(user)
      end
    end
    context 'with invalid params' do
      it 'assigns the user as @user' do
        user = User.create! valid_attributes
        inval_params = { id: user.to_param, user: invalid_attributes }
        put :update, inval_params, valid_session
        expect(assigns(:user)).to eq(user)
      end
    end
  end
  describe 'DELETE #destroy' do
    it 'destroys the requested user' do
      skip
      user = User.create! valid_attributes
      expect {
        delete :destroy, { id: user.to_param }, valid_session
      }.to change(User, :count).by(-1)
    end
    it 'redirects to the users list' do
      skip
      user = User.create! valid_attributes
      delete :destroy, { id: user.to_param }, valid_session
      expect(response).to redirect_to(users_url)
    end
  end
end

```