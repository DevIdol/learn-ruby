### **Ruby on Rails - Views**

Rails ရဲ့ **Views** ဆိုတာ application ရဲ့ frontend UI ကို ပြသရန် အသုံးပြုသော အပိုင်းဖြစ်ပါတယ်။ **Controller** ကနေ data ကို pass လုပ်ပြီး View သည် HTML, CSS, JavaScript အပြင် Rails templates တွေကို အသုံးပြု၍ အဲဒီ data ကို ပြသပေးပါမည်။

Rails ရဲ့ View templates တွေမှာ default အနေဖြင့် **ERB (Embedded Ruby)** format ကို အသုံးပြုသည်။ **HAML**, **Slim** လို template engines များကိုလည်း အသုံးပြုနိုင်သည်။

---

### **View File Location**

View files တွေဟာ **`app/views/`** directory ထဲမှာ သိမ်းဆည်းထားပြီး, Controller နဲ့ ချိတ်ဆက်ထားသည်။

ဥပမာ:
- **BooksController** မှာ **index** action ရှိပါက **`app/views/books/index.html.erb`** file ကို render လုပ်မည်။

---

### **Rendering Views**

#### **1. Automatic Rendering**
Rails သည် Controller မှာ action တစ်ခုစီအတွက် အလိုအလျောက် အဆိုင်အရာကို သက်ဆိုင်ရာ View file မှာ render လုပ်ပေးပါသည်။

ဥပမာ:
```ruby
class BooksController < ApplicationController
  def index
    @books = Book.all
  end
end
```
- **View File**: `app/views/books/index.html.erb`
- **Rendering**: Rails သည် **@books** ကို ERB Template ထဲမှာ render လုပ်ပေးမည်။

#### **2. Manual Rendering**
```ruby
def index
  render "custom_template"
end
```
ဤနည်းစနစ်သည် View template တစ်ခုကို လိုသလို ပြောင်းလဲပြီး render လုပ်ရန် အသုံးပြုနိုင်သည်။

---

### **Passing Data to Views**

Controller ကနေ View file ကို data pass လုပ်ရန် **instance variables (`@`)** ကိုသုံးပါသည်။

#### **Example:**
```ruby
class BooksController < ApplicationController
  def index
    @books = Book.all
  end
end
```

**View File (`index.html.erb`):**
```erb
<h1>Book List</h1>
<ul>
  <% @books.each do |book| %>
    <li><%= book.title %> by <%= book.author %></li>
  <% end %>
</ul>
```

---

### **ERB Syntax**

#### **Ruby Code Embedment**
```erb
<% ruby_code %>        <!-- Executes Ruby code but does not output -->
<%= ruby_code %>       <!-- Executes Ruby code and outputs the result -->
```

#### **Example:**
```erb
<% 3.times do |i| %>
  <p>This is loop number <%= i + 1 %>.</p>
<% end %>
```

#### **Output:**
```
<p>This is loop number 1.</p>
<p>This is loop number 2.</p>
<p>This is loop number 3.</p>
```

---

### **Partial Views**

**Partial Views** သည် View templates တွေကို reusable နည်းဖြင့် စီမံခန့်ခွဲရန် အသုံးပြုသည်။ Partial view files တွေမှာ filename ရှေ့တွင် **underscore (`_`)** ပါသည်။

#### **Example:**
**Partial File (`_book.html.erb`):**
```erb
<li><%= book.title %> by <%= book.author %></li>
```

**Parent View (`index.html.erb`):**
```erb
<ul>
  <% @books.each do |book| %>
    <%= render partial: "book", locals: { book: book } %>
  <% end %>
</ul>
```

**Shortcut:**
```erb
<%= render @books %> <!-- Rails will look for `_book.html.erb` automatically -->
```

---

### **Layouts**

**Layouts** သည် application-wide design သို့မဟုတ် UI structure ကို သတ်မှတ်ရန်အသုံးပြုသည်။ Default Layout file သည် **`app/views/layouts/application.html.erb`** ဖြစ်သည်။

#### **Example Layout:**
```erb
<!DOCTYPE html>
<html>
  <head>
    <title>My Rails App</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>
    <%= stylesheet_link_tag "application", media: "all" %>
  </head>
  <body>
    <%= yield %> <!-- Render the View Template Content -->
  </body>
</html>
```

#### **Yield Example:**
```erb
<h1>Header</h1>
<%= yield :sidebar %> <!-- Custom Content Section -->
<p>Footer</p>
```

**Controller:**
```ruby
def index
  render layout: "custom_layout"
end
```

---

### **Helper Methods**

**Helpers** သည် View တွေမှာ reusable code တွေကို အသုံးပြုစေသည်။

#### **Example Helper Method:**
```ruby
module BooksHelper
  def format_date(date)
    date.strftime("%B %d, %Y")
  end
end
```

**Usage in View:**
```erb
<p>Published on: <%= format_date(book.published_at) %></p>
```

---

### **Using Slim Template**

Slim သည် lightweight template engine တစ်ခုဖြစ်ပြီး ERB ထက် syntax ပိုမိုရိုးရှင်းပါသည်။

#### **Example:**
**ERB Template (`index.html.erb`):**
```erb
<h1>Books</h1>
<ul>
  <% @books.each do |book| %>
    <li><%= book.title %></li>
  <% end %>
</ul>
```

**Slim Template (`index.html.slim`):**
```slim
h1 Books
ul
  - @books.each do |book|
    li = book.title
```

---

### **Example**

#### **Controller:**
```ruby
class BooksController < ApplicationController
  def index
    @books = Book.all
  end
end
```

#### **View (`index.html.erb`):**
```erb
<h1>Book List</h1>
<ul>
  <% @books.each do |book| %>
    <li><%= book.title %> - <%= book.author %></li>
  <% end %>
</ul>
```

---

Rails ရဲ့ **Views** တွေဟာ application ရဲ့ UI ကို render လုပ်ရန်အတွက် အဓိက အခန်းကဏ္ဍထမ်းဆောင်ပေးပါတယ်။  
- **ERB**, **HAML**, နဲ့ **Slim** တို့ကို သုံးနိုင်သည်။
- **Layouts**, **Partials**, နဲ့ **Helpers** သုံးပြီး View templates တွေကို modular နည်းဖြင့် စီမံခန့်ခွဲနိုင်သည်။
- Rails View templates တွေကို dynamic နည်းလမ်းဖြင့် ဖန်တီးပြီး, DRY principle အတိုင်း code ရေးသားနိုင်သည်။