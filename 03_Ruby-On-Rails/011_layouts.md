### **Ruby on Rails - Layouts**

**Layouts** ဆိုတာ Ruby on Rails application ထဲမှာ shared design structure ကို သတ်မှတ်ရန်အသုံးပြုသည်။ Layouts က တစ်ခုတည်းသော HTML skeleton တစ်ခုအနေဖြင့် အသုံးပြုပြီး **yield** လို့ခေါ်တဲ့ placeholder နေရာမှာ specific view templates တွေကို render လုပ်စေပါသည်။ 

ဤနည်းစနစ်က code duplication ကိုလျှော့ချပြီး, **DRY (Don’t Repeat Yourself)** ကိုလည်း လိုက်နာစေပါတယ်။

---

### **Default Layout**

Rails application တွေမှာ default layout သည် **`app/views/layouts/application.html.erb`** ဖြစ်သည်။

#### **Example Layout:**

**`app/views/layouts/application.html.erb`:**
```erb
<!DOCTYPE html>
<html>
  <head>
    <title>My Rails App</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>
    <%= stylesheet_link_tag "application", media: "all" %>
    <%= javascript_include_tag "application" %>
  </head>
  <body>
    <header>
      <h1>Welcome to My App</h1>
    </header>

    <div id="content">
      <%= yield %> <!-- View templates will be rendered here -->
    </div>

    <footer>
      <p>&copy; 2024 My Rails App</p>
    </footer>
  </body>
</html>
```

#### **Explanation:**
1. **`yield`** သည် layout file ထဲမှာ View template rendering အတွက် placeholder အဖြစ်အသုံးပြုသည်။
2. Header, Footer, CSS, JavaScript files တွေကို shared အဖြစ် ထည့်သွင်းထားသည်။

---

### **Specifying Layouts**

#### **1. Controller-Level Layout:**

Controller တစ်ခုတည်းအတွက် layout သတ်မှတ်လိုပါက:
```ruby
class BooksController < ApplicationController
  layout "books"
end
```

ဤ code သည် **`app/views/layouts/books.html.erb`** layout ကို အသုံးပြုမည်။

#### **2. Action-Specific Layout:**
```ruby
class BooksController < ApplicationController
  layout "admin", only: [:edit, :update]
  layout "public", except: [:edit, :update]
end
```

#### **3. Rendering Without Layout:**
```ruby
def index
  render layout: false
end
```

---

### **Custom Layouts**

Layout တစ်ခုကို ဖန်တီးရန် **`app/views/layouts/`** folder ထဲမှာ HTML template file အသစ်တစ်ခုဖန်တီးရပါမည်။

#### **Example:**

**File:** `app/views/layouts/admin.html.erb`
```erb
<!DOCTYPE html>
<html>
  <head>
    <title>Admin Panel</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>
    <%= stylesheet_link_tag "admin", media: "all" %>
  </head>
  <body>
    <header>
      <h1>Admin Dashboard</h1>
    </header>

    <div id="content">
      <%= yield %>
    </div>

    <footer>
      <p>Admin Panel &copy; 2024</p>
    </footer>
  </body>
</html>
```

#### **Controller:**
```ruby
class AdminController < ApplicationController
  layout "admin"
end
```

---

### **Using `content_for`**

Rails မှာ **`content_for`** ကိုအသုံးပြုပြီး layout ထဲမှာ specific section အတွက် custom content ထည့်နိုင်သည်။

#### **Example:**

**Layout File (`application.html.erb`):**
```erb
<!DOCTYPE html>
<html>
  <head>
    <title>My App</title>
    <%= yield :head %> <!-- Custom content for the head section -->
  </head>
  <body>
    <%= yield %> <!-- Main content -->
  </body>
</html>
```

**View File (`index.html.erb`):**
```erb
<% content_for :head do %>
  <meta name="description" content="A description for this page">
<% end %>

<h1>Welcome to the Index Page</h1>
<p>This is the main content.</p>
```

#### **Output:**
```html
<!DOCTYPE html>
<html>
  <head>
    <title>My App</title>
    <meta name="description" content="A description for this page">
  </head>
  <body>
    <h1>Welcome to the Index Page</h1>
    <p>This is the main content.</p>
  </body>
</html>
```

---

### **Nested Layouts**

Layout files တွေကို nested layout အဖြစ် သုံးနိုင်သည်။

#### **Example:**

**Base Layout (`layouts/application.html.erb`):**
```erb
<!DOCTYPE html>
<html>
  <head>
    <title>My App</title>
    <%= yield :head %>
  </head>
  <body>
    <%= yield %>
  </body>
</html>
```

**Admin Layout (`layouts/admin.html.erb`):**
```erb
<% content_for :head do %>
  <link rel="stylesheet" href="/assets/admin.css">
<% end %>

<%= yield %>
```

**Controller:**
```ruby
class AdminController < ApplicationController
  layout "admin"
end
```

---

### **View-Specific Layout**

View တစ်ခုစီအတွက် layout ကို manual rendering ဖြင့် သတ်မှတ်နိုင်သည်။

#### **Example:**
```ruby
def show
  render layout: "special_layout"
end
```

---

### **Testing Layouts**

Layouts သည် Rails view testing framework များဖြင့် စစ်ဆေးနိုင်သည်။

#### **Example:**
```ruby
require "rails_helper"

RSpec.describe "Layouts", type: :request do
  it "renders the application layout" do
    get root_path
    expect(response.body).to include("My Rails App")
  end
end
```

---

- Rails Layouts တွေဟာ application-wide design ကို စနစ်တကျ စီမံခန့်ခွဲပေးပါတယ်။
- Default Layout, Custom Layouts, Nested Layouts, နဲ့ **`content_for`** စသည်တို့ကို အသုံးပြုပြီး လိုအပ်သော UI structure ကို ဖန်တီးနိုင်ပါတယ်။
- Layout တွေက View templates တွေကို shared design framework အနေနဲ့ integrate လုပ်ပေးခြင်းဖြင့် productivity ကို မြှင့်တင်စေသည်။