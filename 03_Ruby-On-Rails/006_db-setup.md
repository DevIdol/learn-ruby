### **Ruby on Rails - Database Setup**

Ruby on Rails application ကို database ဖြင့် ချိတ်ဆက်ဖို့အတွက် **Database Setup** အဆင့်ကို လုပ်ဆောင်ရပါမည်။ Rails တွင် database ကို အထောက်အပံ့ပေးသော **ActiveRecord** ORM (Object Relational Mapping) ကို အသုံးပြုထားပြီး, database schema management ကို လွယ်ကူစေပါတယ်။ 

ဤအပိုင်းတွင် PostgreSQL ကို အသုံးပြုပြီး database setup လုပ်ပုံကို ရှင်းပြပေးပါမယ်။

---

### **1. Database Configuration ဖိုင်**
Rails application ရဲ့ database configuration ကို **`config/database.yml`** ဖိုင်တွင် သတ်မှတ်ထားပါတယ်။ Default Rails application သည် SQLite ကို အသုံးပြုထားပါသည်။

#### **PostgreSQL Setup Example**
**`config/database.yml`** ကို ပြင်ဆင်ပါ။

```yaml
default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: your_db_username
  password: your_db_password
  host: localhost

development:
  <<: *default
  database: my_app_development

test:
  <<: *default
  database: my_app_test

production:
  <<: *default
  database: my_app_production
  username: <%= ENV['MY_APP_DATABASE_USER'] %>
  password: <%= ENV['MY_APP_DATABASE_PASSWORD'] %>
```

---

### **2. PostgreSQL Database Server Installation**
Ruby on Rails တွင် PostgreSQL ကို အသုံးပြုမည်ဆိုပါက PostgreSQL database server ကို သင့် system တွင် ထည့်သွင်းထားရန်လိုအပ်ပါသည်။

**Ubuntu မှာ Install လုပ်ရန်:**
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib libpq-dev
```

**Windows မှာ Install လုပ်ရန်:**
[PostgreSQL Official Website](https://www.postgresql.org/download/) မှ Installer ကို download လုပ်ပြီး install လုပ်ပါ။

**Mac မှာ Install လုပ်ရန် (Homebrew):**
```bash
brew install postgresql
brew services start postgresql
```

---

### **3. Rails Project Database Setup**

#### **Step 1: Gemfile Update**
PostgreSQL adapter gem ကို **Gemfile** တွင် ထည့်သွင်းပါ။

```ruby
gem 'pg', '~> 1.4'
```

**Bundler Command**
```bash
bundle install
```

#### **Step 2: Database Creation**
Database ကို Rails CLI ကို အသုံးပြု၍ ဖန်တီးပါ။

```bash
rails db:create
```

ဒီအဆင့်မှာ development, test database များကို database.yml ဖိုင်အတိုင်း ဖန်တီးပေးပါလိမ့်မယ်။

#### **Step 3: Migrate Database Schema**
Rails application ၏ database schema များကို **migrations** ဖြင့် update လုပ်ပါ။

```bash
rails db:migrate
```

#### **Step 4: Seed Database**
Database ကို Initial Data ဖြင့် populate လုပ်ရန် **`db/seeds.rb`** ဖိုင်ကို အသုံးပြုပါ။

```bash
rails db:seed
```

---

### **4. Database နှင့် ချိတ်ဆက်မှု စမ်းသပ်ခြင်း**

**Rails Console မှ Database နှင့်ချိတ်ဆက်ပါ:**
```bash
rails console
```

Console ထဲတွင် အောက်ပါ code ကို ရိုက်ပါ:
```ruby
ActiveRecord::Base.connection
Book.create(title: 'Rails Guide', author: 'Rails Team')
Book.first
```

Database တစ်ခုကို ချိတ်ဆက်ပြီး model တွေကို CRUD operation လုပ်နိုင်မှ database setup အောင်မြင်ပါပြီ။

---

### **5. Database Setup ကို တိုးချဲ့ခြင်း**

#### **Environment Variables Usage**
Production အတွက် sensitive information (e.g., database username, password) များကို **environment variables** မှာ သိမ်းဆည်းပါ။

**Example (Linux/Mac):**
```bash
export MY_APP_DATABASE_USER="production_user"
export MY_APP_DATABASE_PASSWORD="secure_password"
```

---

### **6. Error Troubleshooting**

**Error: `PG::ConnectionBad`**
- PostgreSQL service ကို Start လုပ်ထားပါမယ်။
```bash
sudo service postgresql start
```

**Error: `FATAL: Role 'username' does not exist`**
- PostgreSQL user ကို ဖန်တီးပါ။
```bash
sudo -u postgres createuser -s your_db_username
sudo -u postgres psql
\password your_db_username
```

---

### **7. Rails Database Management Commands**

1. **Database Creation**:
   ```bash
   rails db:create
   ```
2. **Database Migration**:
   ```bash
   rails db:migrate
   ```
3. **Database Seeding**:
   ```bash
   rails db:seed
   ```
4. **Database Reset**:
   ```bash
   rails db:drop db:create db:migrate
   ```

---

ဒီအဆင့်တိုင်းကို Follow လုပ်ပြီး Rails application ကို PostgreSQL database နဲ့ အဆင်ပြေစွာချိတ်ဆက်နိုင်ပါပြီ။ **Rails ၏ ActiveRecord** ကို အသုံးပြု၍ database interactions များကို လွယ်ကူစွာ ပြုလုပ်နိုင်ပါတယ်။