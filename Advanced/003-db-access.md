### **Ruby/DBI - Database Access with PostgreSQL**

Ruby တွင် PostgreSQL database ကို access ပြုလုပ်ရန် **DBI (Database Interface)** library ကို အသုံးပြုနိုင်ပါတယ်။ DBI က database နှင့် communication ချိတ်ဆက်ရန် အဆင်ပြေတဲ့ interface ဖြစ်ပြီး, Ruby program တွေက PostgreSQL, MySQL, SQLite စတဲ့ relational databases များကို လွယ်ကူစွာ အသုံးပြုနိုင်ပါတယ်။

Ruby တွင် PostgreSQL ကိုအသုံးပြုရန် **`pg` gem** သို့မဟုတ် **`dbi` gem** ကိုအသုံးပြုနိုင်ပါတယ်။ အခု **`pg` gem** ကို အသုံးပြုပြီး PostgreSQL ကို Ruby မှတဆင့် အလွယ်တကူ connect လုပ်ရန်နည်းလမ်းများကို ရှင်းပြပါမည်။

---

### **1. PostgreSQL အတွက် Ruby Gem တွေ သတ်မှတ်ခြင်း**

#### **1.1 pg Gem ကို Install လုပ်ခြင်း**

Ruby PostgreSQL module **`pg`** ကို install လုပ်ရန် Terminal မှာ အောက်ပါ command ကို run လိုက်ပါ။

```bash
gem install pg
```

#### **1.2 Database သတ်မှတ်ချက်များ**

PostgreSQL ကို Ruby တွင် သုံးရန်, database server, user credentials နှင့် database name သတင်းအချက်အလက်များ အကြောင်းလေးကို သိထားဖို့လိုပါတယ်။ PostgreSQL database ရဲ့ configuration သို့မဟုတ် connection parameters တွေမှာ အောက်ပါ data များရှိရပါမည်။

- **Host**: Database server အမည် (localhost)
- **Port**: PostgreSQL default port `5432`
- **Username**: Database username
- **Password**: Database password
- **Database Name**: PostgreSQL database name

---

### **2. Database Connection Establishing**

PostgreSQL database ကို Ruby တွင် **`pg`** gem အသုံးပြုပြီး connection ပြုလုပ်နိုင်ပါတယ်။

```ruby
require 'pg'

begin
  # PostgreSQL database connection
  conn = PG.connect(dbname: 'your_database_name', user: 'your_username', password: 'your_password')

  puts "Connected to the database successfully!"

  # Query execution example
  result = conn.exec("SELECT * FROM your_table_name")

  # Display results
  result.each do |row|
    puts row
  end
rescue PG::Error => e
  puts e.message
ensure
  # Close the connection after use
  conn.close if conn
end
```

**Explanation:**
- `PG.connect` method မှတစ်ဆင့် database နှင့်ချိတ်ဆက်ပါသည်။ `dbname`, `user`, `password` နဲ့ `host` (localhost) ကို အချိန်အတိုင်း ထည့်သွင်းထားသည်။
- `exec` method ကို database query တစ်ခုကို run လုပ်ရန် အသုံးပြုသည်။
- Result ကို `each` loop သုံးပြီး display လုပ်ပါတယ်။

---

### **3. Database Query - Select**

PostgreSQL database မှ data ကို `SELECT` query အသုံးပြုပြီး ရယူနိုင်ပါတယ်။ 

```ruby
require 'pg'

begin
  conn = PG.connect(dbname: 'test_db', user: 'user', password: 'password')

  # SELECT query example
  result = conn.exec("SELECT id, name FROM users")

  result.each do |row|
    puts "ID: #{row['id']}, Name: #{row['name']}"
  end
rescue PG::Error => e
  puts e.message
ensure
  conn.close if conn
end
```

**Explanation:**
- Query `"SELECT id, name FROM users"` သည် `users` table ထဲမှ `id` နှင့် `name` column နှစ်ခုကို ရယူသည်။
- **`result.each`** က result set ကို iterate လုပ်ပြီး record တစ်ခုချင်းစီကို output ပြပေးသည်။

---

### **4. Insert Data into PostgreSQL**

PostgreSQL database မှာ data ထည့်ခြင်း (INSERT) အတွက် **`exec`** method ကို အသုံးပြုနိုင်ပါတယ်။

```ruby
require 'pg'

begin
  conn = PG.connect(dbname: 'test_db', user: 'user', password: 'password')

  # Insert query example
  conn.exec("INSERT INTO users (name, age) VALUES ('John Doe', 30)")

  puts "Data inserted successfully!"
rescue PG::Error => e
  puts e.message
ensure
  conn.close if conn
end
```

**Explanation:**
- `INSERT INTO users (name, age) VALUES ('John Doe', 30)` query သည် `users` table ထဲသို့ name နှင့် age အချက်အလက်ကို insert လုပ်သည်။
- Insert query ကို `exec` method နှင့် run လိုက်သောအခါ PostgreSQL မှ data တစ်ခုလုံးကို တင်သွင်းပါတယ်။

---

### **5. Update Data in PostgreSQL**

PostgreSQL database မှာ data update လုပ်ခြင်း (UPDATE) ကိုလည်း **`exec`** method ကနေ ပြုလုပ်နိုင်ပါတယ်။

```ruby
require 'pg'

begin
  conn = PG.connect(dbname: 'test_db', user: 'user', password: 'password')

  # Update query example
  conn.exec("UPDATE users SET age = 31 WHERE name = 'John Doe'")

  puts "Data updated successfully!"
rescue PG::Error => e
  puts e.message
ensure
  conn.close if conn
end
```

**Explanation:**
- `"UPDATE users SET age = 31 WHERE name = 'John Doe'"` query သည် `users` table မှာ name က `John Doe` ဖြစ်တဲ့ row ရဲ့ `age` ကို 31 အဖြစ် update လုပ်ပါသည်။

---

### **6. Delete Data from PostgreSQL**

Data delete လုပ်ရန် **`exec`** method ကို အသုံးပြု၍ **DELETE** query တစ်ခု run လုပ်နိုင်ပါတယ်။

```ruby
require 'pg'

begin
  conn = PG.connect(dbname: 'test_db', user: 'user', password: 'password')

  # Delete query example
  conn.exec("DELETE FROM users WHERE name = 'John Doe'")

  puts "Data deleted successfully!"
rescue PG::Error => e
  puts e.message
ensure
  conn.close if conn
end
```

**Explanation:**
- `"DELETE FROM users WHERE name = 'John Doe'"` query သည် `users` table မှ `name` က `John Doe` ဖြစ်သော row ကို ဖျက်ပစ်ပါသည်။

---

### **7. Using Prepared Statements**

Prepared statements သည် security reasons (e.g. SQL Injection) ကြောင့် အထူးသဖြင့် **bind parameters** သုံးခြင်းအားဖြင့် parameterized queries အသုံးပြုရာတွင် အသုံးဝင်သည်။

```ruby
require 'pg'

begin
  conn = PG.connect(dbname: 'test_db', user: 'user', password: 'password')

  # Using prepared statement to insert data safely
  conn.prepare('insert_user', 'INSERT INTO users (name, age) VALUES ($1, $2)')
  conn.exec_prepared('insert_user', ['Alice', 28])

  puts "Data inserted successfully!"
rescue PG::Error => e
  puts e.message
ensure
  conn.close if conn
end
```

**Explanation:**
- Prepared statement သည် **`$1`**, **`$2`** စတဲ့ placeholders ကို သတ်မှတ်ထားပြီး, query execute မပြုမီ values တွေကို bind လုပ်နိုင်ပါတယ်။
- **`exec_prepared`** method သည် prepared statement ကို run လုပ်ရာမှာ bind values များကို pass ပြုလုပ်ပေးသည်။

---

### **8. Error Handling**

Database connection တွေကို use လုပ်တဲ့အခါ **error handling** များကို လုပ်ဖို့ အရေးကြီးပါသည်။ Ruby မှာ `begin-rescue-end` block ကို error handling အတွက် အသုံးပြုနိုင်ပါတယ်။

```ruby
require 'pg'

begin
  conn = PG.connect(dbname: 'wrong_db', user: 'wrong_user', password: 'wrong_pass')
  puts "Connected to the database successfully!"
rescue PG::Error => e
  puts "An error occurred: #{e.message}"
ensure
  conn.close if conn
end
```

**Explanation:**
- Database connection သွားရတဲ့အခါ error တက်ပါက **`rescue`** block က error message ကို print ထုတ်ပါမည်။

---

Ruby မှ PostgreSQL database ကို **`pg` gem** သုံးပြီး connection ပြုလုပ်နိုင်ပြီး၊ **select**, **insert**, **update**, **delete** operations များကို လွယ်ကူစွာ ပြုလုပ်နိုင်ပါတယ်။ DBI ကိုသုံးတဲ့နေရာမှာ `pg` gem ကို အသုံးပြုခြင်းဟာ PostgreSQL database နှင့် Ruby applications တွေကို integrated လုပ်တဲ့ အလွန်ထိရောက်သောနည်းလမ်းတစ်ခု ဖြစ်ပါသည်။

PostgreSQL ကို Ruby မှာ ပြုလုပ်တဲ့ queries တွေကို **parameterized** method ဖြင့် secure နှင့် efficient ဖြစ်အောင် query လုပ်နိုင်ပါတယ်။ 