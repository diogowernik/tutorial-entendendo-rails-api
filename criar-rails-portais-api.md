1) Generate model and controller for membership

    rails generate model membership plan:string start_date:date finish_date:date active:boolean price:float trial_active:boolean trial_duration:integer

    rails g scaffold_controller Membership
    
2) routes.rb   

    resources :memberships

3) membership_controller.rb

delete because is for rails not needed for rails-api:

    describe "GET #new" do
    it "assigns a new membership as @membership" do
      get :new, {}, valid_session
      expect(assigns(:membership)).to be_a_new(Membership)
    end
    end

    describe "GET #new" do
    it "assigns a new membership as @membership" do
      get :new, {}, valid_session
      expect(assigns(:membership)).to be_a_new(Membership)
    end
    end

    describe "GET #edit" do
    it "assigns the requested membership as @membership" do
      membership = Membership.create! valid_attributes
      get :edit, {:id => membership.to_param}, valid_session
      expect(assigns(:membership)).to eq(membership)
    end
    end

    it "redirects to the created membership" do
     post :create, {:membership => valid_attributes}, valid_session
     expect(response).to redirect_to(Membership.last)
    end
      
    it "re-renders the 'new' template" do
    post :create, {:membership => invalid_attributes}, valid_session
    expect(response).to render_template("new")
    end

    it "re-renders the 'edit' template" do
    membership = Membership.create! valid_attributes
    put :update, {:id => membership.to_param, :membership => invalid_attributes}, valid_session
    expect(response).to render_template("edit")
    end
    
4) membership_spec.rb




    describe 'is valid when' do
    it 'have all data' do
      Membership.create({plan:"Premium", start_date:2016-02-06 14:09:31, finish_date:2016-02-06 14:09:31, active:true, price:80.00, trial_active:false, trial_duration:0})
      expect(Membership.count).to eql(1)
    end
    end

+ plan: :string
+ start_date: :date
+ finish_date: :date
+ active: :boolean
+ price: :float
+ trial_active: :boolean
+ trial_duration: :integer


controller:

params.require(:usuario).permit(:nome)



