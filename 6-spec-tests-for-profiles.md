## 6 - Specs and Tests for Profiles.

**spec/controllers/profiles_controller_spec.rb**

```ruby
require 'rails_helper'

RSpec.describe ProfilesController, type: :controller do
  let(:valid_attributes) {
    batman = User.create(
      email: 'batman@gothan.io',
      password: 'Senha1234'
    )
    {
      description: 'I\'m not batman!', 
      name: 'Bruce Waine',
      user_id: batman.id
    }
  }

  let(:invalid_attributes) {
    { profile: {} }
  }

  let(:valid_session) { {} }

  describe 'GET #index' do
    it 'assigns all profiles as @profiles' do
      profile = Profile.create! valid_attributes
      get :index, {}, valid_session
      expect(assigns(:profiles)).to eq([profile])
    end
  end
  describe 'GET #show' do
    it 'assigns the requested profile as @profile' do
      profile = Profile.create! valid_attributes
      get :show, { id: profile.to_param }, valid_session
      expect(assigns(:profile)).to eq(profile)
    end
  end
  describe 'POST #create' do
    context 'with valid params' do
      it 'creates a new Profile' do
        expect {
          post :create, { profile: valid_attributes }, valid_session
        }.to change(Profile, :count).by(1)
      end
      it 'redirects to the created profile' do
        skip
        post :create, { profile: valid_attributes }, valid_session
        expect(response).to redirect_to(Profile.last)
      end
    end
    context 'with invalid params' do
      it 'assigns a newly created but unsaved profile as @profile' do
        post :create, { profile: invalid_attributes }, valid_session
        expect(assigns(:profile)).to be_a_new(Profile)
      end
    end
  end
  describe 'PUT #update' do
    context 'with valid params' do
      let(:new_attributes) {
        { description: 'I\'M NOT BRUCE WAINE!', name: 'Batman' }
      }
      it 'updates the requested profile' do
        profile = Profile.create! valid_attributes
        new_params = { id: profile.to_param, profile: new_attributes }
        put :update, new_params, valid_session
        profile.reload
        expect(profile.name).to eql(new_attributes[:name])
        expect(profile.description).to eql(new_attributes[:description])
      end
      it 'assigns the requested profile as @profile' do
        profile = Profile.create! valid_attributes
        val_params = { id: profile.to_param, profile: valid_attributes }
        put :update, val_params, valid_session
        expect(assigns(:profile)).to eq(profile)
      end
      it'redirects to the profile' do
        skip
        profile = Profile.create! valid_attributes
        valid_params = { id: profile.to_param, profile: valid_attributes }
        put(:update, valid_params, valid_session)
        expect(response).to redirect_to(profile)
      end
    end
    context 'with invalid params' do
      it 'assigns the profile as @profile' do
        profile = Profile.create! valid_attributes
        invalid_params = { id: profile.to_param, profile: invalid_attributes }
        put(:update, invalid_params, valid_session)
        expect(assigns(:profile)).to eq(profile)
      end
    end
  end
  describe 'DELETE #destroy' do
    it 'destroys the requested profile' do
      profile = Profile.create! valid_attributes
      expect {
        delete :destroy, { id: profile.to_param }, valid_session
      }.to change(Profile, :count).by(-1)
    end
    it 'redirects to the profiles list' do
      skip
      profile = Profile.create! valid_attributes
      delete :destroy, { id: profile.to_param }, valid_session
      expect(response).to redirect_to(profiles_url)
    end
  end
end
```

**spec/models/profile_spec.rb**

```ruby
require 'rails_helper'

RSpec.describe Profile, type: :model do
  describe 'is invalid when' do
    it 'do not have a name' do
      Profile.create(description: 'Some description here ...')
      expect(Profile.count).to eql(0)
    end
    it 'do not have a description' do
      Profile.create(name: 'Fulano de Tal')
      expect(Profile.count).to eql(0)
    end
  end
  describe 'is valid when' do
    it 'have all fields' do
        batman = User.create(
        email: 'batman@gothan.io',
        password: 'Senha1234'
      )
      Profile.create(
        description: 'I am not bruce ...',
        name: 'Batman',
        user: batman
      )
      expect(Profile.count).to eql(1)
    end
  end
end
```
