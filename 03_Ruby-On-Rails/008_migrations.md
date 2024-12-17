### **Ruby on Rails - Migrations**

**Migrations** ဆိုတာ Rails application တွေမှာ **Database Schema** ကို manage လုပ်ဖို့ ရည်ရွယ်ထားတဲ့ feature ဖြစ်ပါတယ်။ Database tables တွေဖန်တီးခြင်း၊ ပြင်ဆင်ခြင်း၊ ဖျက်ခြင်း အစရှိတဲ့လုပ်ဆောင်ချက်တွေကို **Ruby code** နဲ့ပြုလုပ်နိုင်ပြီး SQL queries ရေးရန် မလိုအပ်တော့ပါ။

---

### **1. Migration ဖန်တီးခြင်း**

Rails CLI ကိုအသုံးပြုပြီး Migration ဖိုင်အသစ်တစ်ခုကို ဖန်တီးပါ။

#### **Command:**
```bash
rails generate migration MigrationName
```

**ဥပမာ: `books` table ကို ဖန်တီးရန်**
```bash
rails generate migration CreateBooks
```

ဤ command သည် **`db/migrate/`** folder ထဲမှာ timestamp ပါသော migration file တစ်ခုကို ဖန်တီးပေးပါမည်။

---

### **2. Migration ဖိုင် ဖွင့်ပြီး ရေးသားခြင်း**

ဖန်တီးထားတဲ့ `CreateBooks` migration file ကို edit လုပ်ပါ။

#### **`db/migrate/20231217000000_create_books.rb`**
```ruby
class CreateBooks < ActiveRecord::Migration[6.1]
  def change
    create_table :books do |t|
      t.string :title
      t.string :author
      t.text :description
      t.timestamps
    end
  end
end
```

**Explanation:**
- **`create_table`**: `books` ဆိုတဲ့ table ကို ဖန်တီးသည်။
- **`t.string`**: title နဲ့ author columns ကို string data type နဲ့ဖန်တီး။
- **`t.text`**: description column ကို text data type နဲ့ဖန်တီး။
- **`t.timestamps`**: created_at နဲ့ updated_at columns ကို auto-create ပြုလုပ်ပေး။

---

### **3. Migration Run ပြုလုပ်ခြင်း**

**Command:**
```bash
rails db:migrate
```

ဤ command သည် migration file ထဲမှာရေးသားထားတဲ့ database schema changes တွေကို database တွင် ပြုလုပ်ပေးပါမည်။

---

### **4. Migration Rollback**

တစ်ခါတစ်ရံ migration ပြုလုပ်မှားခဲ့လျှင် **rollback** လုပ်နိုင်ပါတယ်။

#### **Command:**
```bash
rails db:rollback
```

ဤ command သည် နောက်ဆုံး run လုပ်ထားသော migration ကို ပြန်လည်ဖျက်ပစ်ပါမည်။

**Rollback ပြုလုပ်ပြီး ပြန်လည် Run လုပ်ရန်:**
```bash
rails db:migrate
```

---

### **5. Add Column/Remove Column**

Migration file မှတစ်ဆင့် column အသစ်ထည့်ရန်၊ ဖျက်ရန်ကို လုပ်ဆောင်နိုင်ပါသည်။

#### **Column ထည့်ရန်:**
```bash
rails generate migration AddPublishedDateToBooks published_date:date
```

**`db/migrate/20231217000001_add_published_date_to_books.rb`**
```ruby
class AddPublishedDateToBooks < ActiveRecord::Migration[6.1]
  def change
    add_column :books, :published_date, :date
  end
end
```

Run Command:
```bash
rails db:migrate
```

#### **Column ဖျက်ရန်:**
```bash
rails generate migration RemoveDescriptionFromBooks description:text
```

**`db/migrate/20231217000002_remove_description_from_books.rb`**
```ruby
class RemoveDescriptionFromBooks < ActiveRecord::Migration[6.1]
  def change
    remove_column :books, :description, :text
  end
end
```

Run Command:
```bash
rails db:migrate
```

---

### **6. Rename Table/Column**

#### **Table အမည်ပြောင်းရန်:**
```ruby
def change
  rename_table :old_table_name, :new_table_name
end
```

#### **Column အမည်ပြောင်းရန်:**
```ruby
def change
  rename_column :books, :old_column_name, :new_column_name
end
```

---

### **7. Change Column Data Type**

Column ရဲ့ data type ကို ပြောင်းရန်:

```bash
rails generate migration ChangeDataTypeForPublishedDate
```

**`db/migrate/20231217000003_change_data_type_for_published_date.rb`**
```ruby
class ChangeDataTypeForPublishedDate < ActiveRecord::Migration[6.1]
  def change
    change_column :books, :published_date, :datetime
  end
end
```

Run Command:
```bash
rails db:migrate
```

---

### **8. Schema.rb**

Database schema အခြေအနေအားလုံးကို Rails က **`db/schema.rb`** file အနေနဲ့ သိမ်းဆည်းထားပါသည်။  
ဤ file ကို database ရဲ့ current structure ကို အလွယ်တကူ ကြည့်ရှုနိုင်အောင်ပြုလုပ်ထားပါတယ်။

---

### **9. Database Reset**

Database ကို reset လုပ်ပြီး ပြန်တက်ရန်:

```bash
rails db:drop db:create db:migrate
```

---

### **10. Summary**

- **`rails generate migration`**: Migration ဖန်တီးရန်။
- **`rails db:migrate`**: Schema changes တွေကို apply လုပ်ရန်။
- **`rails db:rollback`**: Schema changes တွေကို undo ပြုလုပ်ရန်။
- **`add_column` / `remove_column`**: Columns တွေကို ထည့်ရန်/ဖျက်ရန်။
- **`rename_table` / `rename_column`**: Table နှင့် Column များကို ပြောင်းရန်။
- **`change_column`**: Column data type ပြောင်းရန်။

---

Rails Active Record Migrations က database schema management ကို code နှင့် manage လုပ်နိုင်စေပြီး team collaboration အတွက် လွယ်ကူစေပါတယ်။ **Database schema ကို version control ဖြင့် manage လုပ်ရန် Rails တွင် မရှိမဖြစ် feature တစ်ခုဖြစ်ပါတယ်။**