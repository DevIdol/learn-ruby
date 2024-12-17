### **Ruby on Rails - Send Emails**

Ruby on Rails တွင် Email ပို့ခြင်းသည် **ActionMailer** ကို အသုံးပြုခြင်းဖြင့် အလွယ်တကူ ပြုလုပ်နိုင်ပါတယ်။ **ActionMailer** သည် Rails တွင် built-in feature အဖြစ် ပါဝင်ပြီး၊ email များကို client များသို့ ပို့ခြင်း၊ email template များကို ရေးဆွဲခြင်း၊ ပို့လွှတ်ခြင်းအတွက်အကူအညီပေးပါသည်။

Rails မှာ email ပို့ဖို့အတွက်, မူလအစ ၏ **SMTP (Simple Mail Transfer Protocol)** configuration ကို ရေးဆွဲပြီး အဆင်ပြေသော method များဖြင့် email များကို ပြုလုပ်နိုင်ပါသည်။

---

### **ActionMailer Setup**

#### 1. **Configure Email Settings**

Rails application မှာ email ပို့ရန်အတွက်, `config/environments/development.rb` နှင့် `config/environments/production.rb` ဖိုင်များတွင် email service provider settings များကို configure လုပ်ပါ။

**Development Environment Settings (SMTP)**

```ruby
# config/environments/development.rb

Rails.application.configure do
  config.action_mailer.delivery_method = :smtp
  config.action_mailer.smtp_settings = {
    address: 'smtp.gmail.com',   # SMTP server address (Gmail Example)
    port: 587,                   # Port number
    domain: 'gmail.com',         # Domain for your email
    user_name: ENV['GMAIL_USERNAME'],  # Your Gmail username
    password: ENV['GMAIL_PASSWORD'],  # Your Gmail password
    authentication: 'plain',     # Authentication method
    enable_starttls_auto: true   # Enable TLS encryption
  }
end
```

**Production Environment Settings**

```ruby
# config/environments/production.rb

Rails.application.configure do
  config.action_mailer.delivery_method = :smtp
  config.action_mailer.smtp_settings = {
    address: 'smtp.gmail.com',
    port: 587,
    domain: 'yourdomain.com',
    user_name: ENV['GMAIL_USERNAME'],
    password: ENV['GMAIL_PASSWORD'],
    authentication: 'plain',
    enable_starttls_auto: true
  }
end
```

- **SMTP server**: Gmail, SendGrid, Mailgun, etc. SMTP servers ကို သုံးနိုင်သည်။
- **Environment Variables**: `GMAIL_USERNAME` နဲ့ `GMAIL_PASSWORD` ဆိုပြီး `config/secrets.yml` သို့မဟုတ် `.env` မှာထားသော credentials တွေကို အသုံးပြုသင့်ပါသည်။

---

### **Create Mailer Class**

#### 2. **Generate Mailer**

Rails မှာ `ActionMailer` ကို အသုံးပြုရန်အတွက်, mailer class ကို generate လုပ်ရပါမည်။

```bash
rails generate mailer UserMailer
```

ဒီ command က `app/mailers/user_mailer.rb` ဆိုတဲ့ file ကို generate လုပ်ပါသည်။ ထို့နောက်, `UserMailer` class ထဲတွင် email content များကို define လုပ်မယ်။

#### 3. **Define Methods in Mailer**

Mailer class ကို ရေးသားပြီး email တွေကို ပို့တဲ့ method များကို ဖော်ပြပါ။

```ruby
# app/mailers/user_mailer.rb
class UserMailer < ApplicationMailer
  default from: 'no-reply@yourdomain.com'

  # Welcome email method
  def welcome_email(user)
    @user = user
    @url  = 'http://yourdomain.com/login'
    mail(to: @user.email, subject: 'Welcome to Our Platform!')
  end

  # Password reset email method
  def reset_password_email(user)
    @user = user
    @url  = 'http://yourdomain.com/password_reset'
    mail(to: @user.email, subject: 'Password Reset Instructions')
  end
end
```

- **`default from:`**: email ပို့တဲ့နေရာမှ `from` email address ကို define လုပ်ပါတယ်။
- **`welcome_email(user)`**: `user` object ကို parameter အနေနဲ့ pass လုပ်ပြီး, welcome email ပို့ပါတယ်။
- **`mail(to: @user.email, subject: '...')`**: `to` နဲ့ `subject` များကို pass လုပ်ပြီး email ပို့မည် ဖြစ်သည်။

---

### **Email Views**

#### 4. **Create Email Views (HTML and Text)**

Rails မှာ email template များကို **views** folder အတွင်း **mailer** နာမည်ဖြင့် ဖိုင်များ တည်ဆောက်နိုင်ပါတယ်။ email တစ်ခုကို HTML template နှင့် text template နှစ်ခုလုံးရေးဆွဲနိုင်သည်။

1. **HTML Template for Welcome Email**

```erb
<!-- app/views/user_mailer/welcome_email.html.erb -->
<h1>Welcome to Our Platform, <%= @user.name %>!</h1>
<p>
  We're excited to have you on board. To get started, please click the link below:
</p>
<p>
  <%= link_to 'Login', @url %>
</p>
```

2. **Text Template for Welcome Email**

```text
# app/views/user_mailer/welcome_email.text.erb
Welcome to Our Platform, <%= @user.name %>!

We're excited to have you on board. To get started, please visit the following URL:
<%= @url %>
```

- **HTML version**: Email content ကို HTML markup များနဲ့ ဖော်ပြထားပြီး, link များကို clickable ဖြစ်အောင် လုပ်နိုင်ပါတယ်။
- **Text version**: Text version သည် plain text ဖော်ပြထားပြီး, email clients အများစုတွင် compatibility ရှိပါတယ်။

---

### **Sending Emails**

#### 5. **Sending Email from Controller**

`UserMailer` class ထဲမှာ email method ကို call လုပ်ပြီး email ပို့နိုင်ပါတယ်။

```ruby
# app/controllers/users_controller.rb
class UsersController < ApplicationController
  def create
    @user = User.new(user_params)
    if @user.save
      # Send Welcome Email
      UserMailer.welcome_email(@user).deliver_later
      redirect_to @user, notice: 'User was successfully created.'
    else
      render :new
    end
  end

  private

  def user_params
    params.require(:user).permit(:name, :email, :password)
  end
end
```

- **`deliver_later`**: Email ကို background job အဖြစ် asynchronous ပေးပို့ရန် `deliver_later` method ကို အသုံးပြုပါသည်။ Rails မှာ email ပို့ခြင်းကို background jobs (Sidekiq, ActiveJob, etc.) နှင့်လည်း အလုပ်လုပ်နိုင်သည်။
- **`deliver_now`**: Email ကို synchronous ပို့ချင်ရင် `deliver_now` ကိုအသုံးပြုနိုင်ပါတယ်။

---

### **Testing Email in Development**

#### 6. **Preview Emails in Development**

Rails ၏ development mode တွင် emails များကို **rails console** သို့မဟုတ် **email previews** နဲ့ test လုပ်နိုင်ပါသည်။

1. **Email Previews**: Rails မှာ emails ကို development mode တွင် browser မှာ preview လုပ်နိုင်ပါသည်။ `app/mailers` directory အတွင်း `preview` folder တစ်ခုဖန်တီးပြီး၊ previews ရေးဆွဲပါ။

```ruby
# app/mailers/previews/user_mailer_preview.rb
class UserMailerPreview < ActionMailer::Preview
  def welcome_email
    user = User.first
    UserMailer.welcome_email(user)
  end
end
```

- `http://localhost:3000/rails/mailers/user_mailer/welcome_email` မှာ preview ကိုကြည့်နိုင်ပါသည်။

2. **Console Testing**:

```ruby
user = User.first
UserMailer.welcome_email(user).deliver_now
```

- ဒီ command မှာ `UserMailer.welcome_email` method ကို console မှာ call လုပ်ပြီး email ကို test ပို့နိုင်ပါသည်။

---

### **Handling Attachments**

#### 7. **Email Attachments**

Rails မှာ attachment တွေကို email နဲ့တစ်ပြိုင်နက် ပို့နိုင်ပါတယ်။ attachment ကို **`attachments`** method သုံးပြီး လုပ်ဆောင်နိုင်ပါသည်။

```ruby
class UserMailer < ApplicationMailer
  def send_report(user)
    @user = user
    attachments['report.pdf'] = File.read('/path/to/report.pdf')
    mail(to: @user.email, subject: 'Your Report')
  end
end
```

- **`attachments['report.pdf']`**: File path မှာရှိတဲ့ PDF file ကို email နဲ့ attach လုပ်ပါသည်။

---

Ruby on Rails မှာ email ပို့ခြင်းသည် **ActionMailer** ကို အသုံးပြုပြီး အလွယ်တကူလုပ်ဆောင်နိုင်ပါသည်။ SMTP configuration ကို set up လုပ်ပြီး၊ mailer class တွေ၊ email views တွေကို define လုပ်ပြီး controller မှာ email ပို့ရန် method များကို call လုပ်နိုင်ပါသည်။ Rails ၏ **background jobs** နှင့် ပေါင်းပြီး email ပို့မှုများကို asynchronous ပုံစံဖြင့်လုပ်ဆောင်နိုင်ပါတယ်။ **attachments** နဲ့ email ပို့ခြင်း၊ **email previews** ကိုလည်း testing purposes အတွက် အသုံးပြုနိုင်ပါသည်။