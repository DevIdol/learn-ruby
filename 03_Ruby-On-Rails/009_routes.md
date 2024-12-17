### **Ruby on Rails - Routes**

Rails မှာ **Routes** ဆိုတာ **URL** တွေနဲ့ **Controller Actions** တွေကို mapping လုပ်ပေးတဲ့ အစိတ်အပိုင်းဖြစ်ပါတယ်။ **Routing** က user request ကို application ရဲ့ မည်သည့် controller action ထံပို့ရမလဲဆိုတာကို သတ်မှတ်ပေးပါသည်။  

Rails routing ရဲ့ configuration file က **`config/routes.rb`** မှာ ရှိပါတယ်။

---

### **Basic Syntax**

```ruby
Rails.application.routes.draw do
  get "controller_name/action_name"
end
```

ဥပမာ:
```ruby
Rails.application.routes.draw do
  get "books/index"
end
```

ဤ code က `http://localhost:3000/books/index` URL request ကို **BooksController** ရဲ့ **index** action ထံပို့ပေးပါမည်။

---

### **RESTful Routes**

Rails မှာ **resources** ဆိုတဲ့ shortcut ကိုအသုံးပြုခြင်းဖြင့် RESTful routes တွေကို အလွယ်တကူ ဖန်တီးနိုင်ပါတယ်။

```ruby
resources :books
```

ဤ code ကအောက်ပါ routes တွေကို ဖန်တီးပေးပါမည်:

| HTTP Method | Path         | Controller#Action  | Description                   |
|-------------|--------------|--------------------|-------------------------------|
| GET         | /books       | books#index        | Display all books             |
| GET         | /books/new   | books#new          | Display form for new book     |
| POST        | /books       | books#create       | Create a new book             |
| GET         | /books/:id   | books#show         | Display a specific book       |
| GET         | /books/:id/edit | books#edit       | Display form to edit book     |
| PATCH/PUT   | /books/:id   | books#update       | Update a specific book        |
| DELETE      | /books/:id   | books#destroy      | Delete a specific book        |

---

### **Custom Routes**

#### **1. Simple Route:**
```ruby
get "books/list", to: "books#index"
```
URL: `/books/list` ကို **BooksController** ရဲ့ **index** action ဆီပို့မည်။

#### **2. Route with Dynamic Segments:**
```ruby
get "books/:id", to: "books#show"
```
URL မှာ **`:id`** parameter ရှိပါမည်။  
ဥပမာ: `/books/1` => **BooksController** ရဲ့ **show** action ကို params[:id] = 1 နဲ့ ပို့မည်။

#### **3. Named Routes:**
```ruby
get "books/:id/details", to: "books#details", as: "book_details"
```
**book_details_path(id: 1)** ဟု helper method အနေနဲ့အသုံးပြုနိုင်သည်။

---

### **Root Route**

Application ရဲ့ main page ကိုသတ်မှတ်ရန်:
```ruby
root "books#index"
```
ဤ code က application ရဲ့ **http://localhost:3000/** ကို **BooksController** ရဲ့ **index** action ကိုပို့ပါမည်။

---

### **Route Constraints**

Request တစ်ခုကို constraint ပြုလုပ်ပြီး specific condition များအတိုင်း handle လုပ်နိုင်သည်။

#### **Example:**
```ruby
get "books/:id", to: "books#show", constraints: { id: /\d+/ }
```
ဤ route က id သည် **digit** (0-9) သာဖြစ်ရမည်။

---

### **Nested Routes**

Association တွေရှိသော models များအတွက် nested routes အသုံးပြုနိုင်သည်။

#### **Example:**
```ruby
resources :authors do
  resources :books
end
```

ဤ code ကအောက်ပါ routes တွေကို ဖန်တီးပါမည်:

| HTTP Method | Path                        | Controller#Action         |
|-------------|-----------------------------|---------------------------|
| GET         | /authors/:author_id/books   | books#index               |
| GET         | /authors/:author_id/books/:id | books#show              |

---

### **Namespace Routes**

Namespace သုံးပြီး admin panel သို့မဟုတ် API logic အတွက် routes ကို grouping ပြုလုပ်နိုင်သည်။

#### **Example:**
```ruby
namespace :admin do
  resources :books
end
```

ဤ code က admin panel အတွက် အောက်ပါ routes ကိုဖန်တီးပါမည်:
- **/admin/books**
- **Admin::BooksController**

---

### **Route Helpers**

Rails မှာ route helpers က URL တွေကို အလွယ်တကူပြုလုပ်နိုင်စေသည်။

#### **Example:**
```ruby
resources :books
```

| Helper Method           | Generated Path       |
|-------------------------|----------------------|
| books_path              | /books              |
| new_book_path           | /books/new          |
| edit_book_path(@book)   | /books/:id/edit     |
| book_path(@book)        | /books/:id          |

---

### **HTTP Verb Matching**

Routes ကို specific HTTP methods နဲ့ပဲ match လုပ်ချင်သောအခါ:
```ruby
post "books/create", to: "books#create"
put "books/:id/update", to: "books#update"
delete "books/:id", to: "books#destroy"
```

---

### **Route Testing**

Routes မှန်ကန်ကြောင်းစစ်ရန်:
```bash
rails routes
```
ဤ command သည် application ထဲရှိ ရရှိနိုင်သော routes များအားလုံးကို ဖော်ပြပါမည်။

---

### **Example Routes File**

#### **`config/routes.rb`**
```ruby
Rails.application.routes.draw do
  root "books#index"

  resources :books do
    member do
      get "preview"
    end

    collection do
      get "search"
    end
  end

  namespace :admin do
    resources :authors
  end
end
```

---

Rails Routes တွေဟာ application ရဲ့ URL တွေနဲ့ Controller logic တွေကို စနစ်တကျ တစ်နေရာတည်းမှာ သတ်မှတ်ပြီး manage လုပ်စေပါတယ်။  
**RESTful routes**, **custom routes**, **nested routes**, နဲ့ **namespace routes** တို့အားအသုံးပြုခြင်းဖြင့် application ကိုအဆင်ပြေစွာ တည်ဆောက်နိုင်ပါသည်။