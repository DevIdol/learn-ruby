### **Ruby on Rails - File Uploading**

Ruby on Rails မှာ file upload ကို implement လုပ်ရာတွင် `ActiveStorage` ကို အသုံးပြုနိုင်ပါတယ်။ ActiveStorage သည် Rails 5.2 မှာအသစ်စက်စက်ပါဝင်လာပြီး၊ files များကို server တွင် သိမ်းဆည်းခြင်း သို့မဟုတ် cloud storage service များ (Amazon S3, Google Cloud, Microsoft Azure, etc.) တွင် upload လုပ်သိမ်းထားနိုင်သည်။

ActiveStorage ကို သုံးခြင်းဖြင့် **image**, **documents**, **audio** files များကို ဖိုင်စနစ်တွင် upload ပြုလုပ်နိုင်သည်။

---

### **File Uploading Setup in Rails (ActiveStorage)**

#### 1. **ActiveStorage Installation**

Rails project အတွက် `ActiveStorage` ကို အစဉ်အလာအတိုင်း ဖိုင် upload လုပ်ဖို့ အရင်ဆုံး setup လုပ်ရပါမည်။

- Rails 5.2 အထက် version တွေကို အသုံးပြုထားသေးလျှင် `ActiveStorage` က အလိုအလျောက် install ဖြစ်နေပါသည်။ သို့သော် စတင်ပြုလုပ်ရန် `rails active_storage:install` command ကို run လုပ်ရန်လိုအပ်သည်။

```bash
rails active_storage:install
```

ဒီ command က **migrations** တွေကို generate လုပ်ပေးပြီး၊ database အတွက် `active_storage_blobs` နှင့် `active_storage_attachments` table များကို create လုပ်ပေးပါသည်။

- **active_storage_blobs**: ဖိုင် metadata (filename, content type, etc.) ကို သိမ်းဆည်းထားသည်။
- **active_storage_attachments**: Models တွေကို file များနှင့် link ပြုလုပ်ခြင်း (attachment) ဆက်သွယ်မှုကို သိမ်းဆည်းထားသည်။

#### 2. **Run the Migration**

Database tables တွေကို create လုပ်ဖို့ migration ကို run လုပ်ပါ။

```bash
rails db:migrate
```

---

### **File Uploading in Model**

#### 3. **Model Setup**

Rails model တွင် `has_one_attached` သို့မဟုတ် `has_many_attached` method ကို အသုံးပြု၍ file များကို attach လုပ်နိုင်ပါတယ်။

- **has_one_attached**: တစ်ခုတည်းသော file ကို attach လုပ်ရန် အသုံးပြုသည် (e.g. single image, document, etc.)
- **has_many_attached**: အများအပြား file များကို attach လုပ်ရန် အသုံးပြုသည် (e.g. multiple images, multiple documents, etc.)

**Example for Single File Upload:**

```ruby
class User < ApplicationRecord
  has_one_attached :avatar
end
```

- ဒီအတွက် `avatar` ဆိုတဲ့ field သည် User model တစ်ခု၏ attribute ဖြစ်ပြီး၊ တစ်ခုတည်းသော file ကို attach လုပ်ပါသည်။

**Example for Multiple File Upload:**

```ruby
class Product < ApplicationRecord
  has_many_attached :images
end
```

- ဒီအတွက် `images` ဆိုတဲ့ attribute ကို အသုံးပြုပြီး၊ multiple files (image files) များကို attach လုပ်နိုင်ပါသည်။

---

### **File Uploading in Form**

#### 4. **Form Setup**

Rails တွင် form တွေကို file upload ဖြင့် handle လုပ်ရန် `form_with` helper ကို အသုံးပြုနိုင်ပါတယ်။

- **Single file upload (using `has_one_attached`)**

```erb
<%= form_with(model: @user, local: true) do |form| %>
  <%= form.label :avatar %>
  <%= form.file_field :avatar %>
  <%= form.submit %>
<% end %>
```

- **Multiple file upload (using `has_many_attached`)**

```erb
<%= form_with(model: @product, local: true) do |form| %>
  <%= form.label :images %>
  <%= form.file_field :images, multiple: true %>
  <%= form.submit %>
<% end %>
```

- `multiple: true` option ကို file input field တွင် ထည့်ပေးခြင်းဖြင့် တစ်ခါတည်း multiple files များကို upload လုပ်နိုင်ပါသည်။

---

### **File Uploading in Controller**

#### 5. **Controller Setup**

File upload လုပ်ရာတွင်, controller ထဲမှာ file parameter ကို handle လုပ်ရပါမည်။ ဥပမာ:

```ruby
class UsersController < ApplicationController
  def create
    @user = User.new(user_params)
    if @user.save
      redirect_to @user, notice: 'User was successfully created.'
    else
      render :new
    end
  end

  private

  def user_params
    params.require(:user).permit(:name, :email, :avatar)
  end
end
```

- **user_params** method မှာ `avatar` field ကို permit လုပ်ထားပါသည်။

---

### **Displaying Uploaded Files**

#### 6. **Displaying Files in Views**

Rails သည် uploaded file များကို **image_tag** သို့မဟုတ် **link_to** helper များကို အသုံးပြု၍ display လုပ်နိုင်ပါတယ်။

- **Displaying Single Image (e.g., Avatar)**

```erb
<%= image_tag @user.avatar %>
```

- **Displaying Multiple Images (e.g., Product Images)**

```erb
<% @product.images.each do |image| %>
  <%= image_tag image %>
<% end %>
```

- **Displaying Links to Files**

```erb
<%= link_to 'Download Avatar', rails_blob_path(@user.avatar, disposition: 'attachment') if @user.avatar.attached? %>
```

- **rails_blob_path** helper ကို အသုံးပြုပြီး file ကို download လုပ်နိုင်သော link ကို generate လုပ်နိုင်ပါသည်။

---

### **Handling File Validation**

#### 7. **Validating File Type and Size**

Rails မှာ file validation များကို model level တွင် စိတ်ကြိုက် implement လုပ်နိုင်ပါသည်။ ဥပမာ:

- **File Type Validation**

```ruby
class User < ApplicationRecord
  has_one_attached :avatar
  validates :avatar, content_type: ['image/png', 'image/jpg', 'image/jpeg']
end
```

- **File Size Validation**

```ruby
class User < ApplicationRecord
  has_one_attached :avatar
  validates :avatar, size: { less_than: 5.megabytes, message: 'is too large' }
end
```

- အထက်ပါ validation များက avatar file ၏ content type နှင့် file size ကို validate လုပ်ထားပါသည်။

---

### **File Uploading with Cloud Storage**

#### 8. **Cloud Storage Setup (e.g., Amazon S3)**

Rails တွင် **ActiveStorage** ကို Amazon S3 အပါအဝင် cloud storage services များနှင့်အသုံးပြုနိုင်ပါသည်။ Amazon S3 နှင့်အတူ file uploading ကို configure လုပ်ရန် အောက်ပါအဆင့်များကို လိုက်နာပါ:

1. **Add gems to Gemfile**

   ```ruby
   gem 'aws-sdk-s3', require: false
   gem 'image_processing', '~> 1.2'
   ```

2. **Configure `config/storage.yml`**

   ```yaml
   amazon:
     service: S3
     access_key_id: <%= ENV['AWS_ACCESS_KEY_ID'] %>
     secret_access_key: <%= ENV['AWS_SECRET_ACCESS_KEY'] %>
     region: 'us-west-2'
     bucket: 'your-bucket-name'
   ```

3. **Set ActiveStorage to use Amazon S3 in `config/environments/production.rb`**

   ```ruby
   config.active_storage.service = :amazon
   ```

4. **Set Environment Variables**

   AWS credentials များကို `.env` file မှာ ထည့်ထားနိုင်သည်။

---

Ruby on Rails မှာ **file uploading** ကို **ActiveStorage** နည်းပညာဖြင့် အလွယ်တကူ handle လုပ်နိုင်ပါတယ်။ ဖိုင် upload လုပ်ရာတွင် model တွင် `has_one_attached` သို့မဟုတ် `has_many_attached` ကိုအသုံးပြုပြီး၊ file fields များကို form မှာ `file_field` helper နဲ့ display လုပ်နိုင်ပြီး၊ controller ထဲမှာ `params` များကို handle လုပ်ပါသည်။ Rails ၏ **ActiveStorage** ကို cloud storage (Amazon S3, Google Cloud, etc.) တွေနဲ့ချိတ်ဆက်၍ files များကို cloud ထဲသို့ upload လုပ်နိုင်ပါတယ်။