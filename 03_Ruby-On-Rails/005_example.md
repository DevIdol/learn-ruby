Ruby on Rails ၏ **Examples** များကို `slim` template engine ကို အသုံးပြု၍ ရေးသားနိုင်ပါသည်။ Slim သည် Ruby on Rails တွင် အသုံးပြုနိုင်သော **lightweight template engine** တစ်ခုဖြစ်ပြီး, HTML structure ကို အရမ်းသာ ရှင်းလင်းစွာ ရေးသားနိုင်စေပါတယ်။ အောက်တွင် **Ruby on Rails Example** အချို့ကို Slim template အသုံးပြုပြီး ရေးပြထားပါတယ်။

---

### **1. Slim Setup in Rails**

#### **Step 1: Slim Gem ထည့်သွင်းပါ**
Slim ကို Rails project တစ်ခုတွင် အသုံးပြုရန် `Gemfile` မှာ gem ကို ထည့်ရန်လိုအပ်ပါတယ်။

```ruby
# Gemfile
gem 'slim-rails'
```

**Command**:
```bash
bundle install
```

#### **Step 2: View File Name Change**
Rails ရဲ့ View files တွင် `.html.erb` format ကို အသုံးပြုသည့်အစား `.html.slim` format ကို အသုံးပြုရပါမယ်။

---

### **2. Example: Basic CRUD Application**

#### **Model - User**
User Model ကို Rails generator ဖြင့် ဖန်တီးပါ:

```bash
rails generate model User name:string email:string
rails db:migrate
```

---

#### **Controller - UsersController**
UsersController ကို ဖန်တီးပြီး CRUD actions များကို ထည့်သွင်းပါ။

```bash
rails generate controller Users
```

**`app/controllers/users_controller.rb`**:
```ruby
class UsersController < ApplicationController
  def index
    @users = User.all
  end

  def new
    @user = User.new
  end

  def create
    @user = User.new(user_params)
    if @user.save
      redirect_to users_path, notice: 'User created successfully!'
    else
      render :new
    end
  end

  private

  def user_params
    params.require(:user).permit(:name, :email)
  end
end
```

---

#### **Routes**
**`config/routes.rb`**:
```ruby
Rails.application.routes.draw do
  resources :users, only: [:index, :new, :create]
end
```

---

### **3. Slim Templates**

#### **Index Page**
**`app/views/users/index.html.slim`**:
```slim
h1 Users List

- if @users.any?
  table
    thead
      tr
        th Name
        th Email
    tbody
      - @users.each do |user|
        tr
          td = user.name
          td = user.email
- else
  p No users found.

= link_to 'New User', new_user_path, class: 'btn btn-primary'
```

---

#### **New User Form**
**`app/views/users/new.html.slim`**:
```slim
h1 New User

= form_with model: @user, local: true do |f|
  .form-group
    = f.label :name
    = f.text_field :name, class: 'form-control'

  .form-group
    = f.label :email
    = f.email_field :email, class: 'form-control'

  = f.submit 'Create User', class: 'btn btn-success'

= link_to 'Back to Users', users_path, class: 'btn btn-secondary'
```

---

### **4. Result**

#### **Index Page** (Users List)
- **Table** တွင် စာရင်းပြသည်။
- "New User" button နှင့် Form ပေါ်သွားနိုင်သည်။

#### **New User Form**
- User name နှင့် email ထည့်ပြီး Submit လုပ်ပါက Database တွင် ထည့်သွင်းမည်။

---

### **5. Slim Advantages**
1. **သွက်လက်သော Syntax**: HTML structure ရေးရာတွင် ရှင်းလင်းပြီး Productivity တိုးတက်စေသည်။
2. **Indentation-Based**: Closing tags မလိုပါဘဲ Indentation သုံးပြီး Structure ထိန်းထားနိုင်သည်။
3. **Faster Development**: Ruby code နှင့် HTML ကို ပေါင်းစပ်ရေးသားရာမှာ အချိန်လျှော့စေသည်။

---

ဒီလိုနည်းဖြင့် Ruby on Rails application တစ်ခုကို Slim template engine အနေနဲ့ ရိုးရှင်းစွာ setup ပြုလုပ်နိုင်ပြီး, Slim ရဲ့ လက်လှမ်းမှီ syntax ကို အသုံးပြု၍ View layer ကို အထူးမိုက်စွာဖန်တီးနိုင်ပါသည်။