### **Ruby on Rails - Active Record**

Rails framework ရဲ့ အဓိက feature တစ်ခုဖြစ်တဲ့ **Active Record** ဟာ database ကို handle လုပ်ပေးတဲ့ ORM (Object Relational Mapping) ဖြစ်ပါတယ်။ **Active Record** က object-oriented programming နဲ့ relational database အကြားက interface ဖြစ်ပြီး database tables နဲ့ Rails application ရဲ့ models တွေကို ချိတ်ဆက်ပေးပါတယ်။

---

### **Active Record ရဲ့ အဓိက Concepts**

1. **Model**  
   Model က database table ကို တစ်ခုတည်းသော class အနေနဲ့ represent လုပ်ပေးပါတယ်။  
   ဥပမာ: `Book` model က **books** ဆိုတဲ့ database table ကို ကိုယ်စားပြုပါတယ်။

2. **Column and Attributes**  
   Database table ရဲ့ columns တွေဟာ Active Record model ရဲ့ attributes အနေနဲ့ map လုပ်ပေးပါတယ်။

3. **CRUD Operations**  
   Active Record ဟာ **Create, Read, Update, Delete (CRUD)** operations တွေကို လွယ်ကူစွာ ပြုလုပ်နိုင်စေပါတယ်။

4. **Migrations**  
   Database schema ကို manage လုပ်ဖို့ Rails Active Record က **migrations** ဆိုတဲ့ feature ကို အသုံးပြုပါတယ်။

---

### **Active Record Model ဖန်တီးခြင်း**

#### **Model Generation Command**
```bash
rails generate model ModelName column1:type column2:type
```

**ဥပမာ: Book Model**
```bash
rails generate model Book title:string author:string description:text
rails db:migrate
```

---

### **Active Record Methods**

#### **1. Create**

**အသစ်သော record ဖန်တီးရန်**
```ruby
book = Book.new(title: "The Ruby Way", author: "Hal Fulton", description: "Learn Ruby comprehensively.")
book.save
```

**သို့မဟုတ်**
```ruby
Book.create(title: "Eloquent Ruby", author: "Russ Olsen", description: "Learn elegant Ruby practices.")
```

---

#### **2. Read**

**All Records ကို Retrieve လုပ်ရန်**
```ruby
books = Book.all
```

**တစ်ခုချင်းစီကို Retrieve လုပ်ရန်**
```ruby
book = Book.find(1) # ID 1 နဲ့ book ကို ဖမ်းမယ်။
```

**Condition ကို သုံးပြီး Query ရှာဖွေမှု**
```ruby
book = Book.find_by(title: "The Ruby Way")
books = Book.where(author: "Russ Olsen")
```

---

#### **3. Update**

**တစ်ခုတည်းသော Record ကို Update လုပ်ရန်**
```ruby
book = Book.find(1)
book.update(title: "Updated Title")
```

**သို့မဟုတ်**
```ruby
Book.where(author: "Russ Olsen").update_all(author: "Updated Author")
```

---

#### **4. Delete**

**တစ်ခုတည်းသော Record ကို Delete**
```ruby
book = Book.find(1)
book.destroy
```

**သို့မဟုတ်**
```ruby
Book.where(author: "Updated Author").destroy_all
```

---

### **Associations (အခိုင်အမာဆက်စပ်မှုများ)**

Active Record မှာ database tables တွေကြားရှိ relationship များကို handle လုပ်ရန် **Associations** ကို အသုံးပြုပါတယ်။

1. **One-to-Many Relationship**
   ```ruby
   class Author < ApplicationRecord
     has_many :books
   end

   class Book < ApplicationRecord
     belongs_to :author
   end
   ```

2. **Many-to-Many Relationship**
   ```ruby
   class Book < ApplicationRecord
     has_and_belongs_to_many :categories
   end

   class Category < ApplicationRecord
     has_and_belongs_to_many :books
   end
   ```

3. **One-to-One Relationship**
   ```ruby
   class User < ApplicationRecord
     has_one :profile
   end

   class Profile < ApplicationRecord
     belongs_to :user
   end
   ```

---

### **Migrations**

Database schema ကို ပြောင်းလဲဖို့ **migrations** ကို အသုံးပြုပါတယ်။

#### **Migration ဖန်တီးရန်**
```bash
rails generate migration AddColumnNameToTableName column_name:data_type
```

#### **Migration ကို Run လုပ်ရန်**
```bash
rails db:migrate
```

---

### **Callbacks**

Active Record model ထဲမှာ callbacks ကို သုံးပြီး record တွေ save လုပ်တဲ့အချိန်၊ update လုပ်တဲ့အချိန်မှာ logic တွေ ရေးနိုင်ပါတယ်။

**ဥပမာ:**
```ruby
class Book < ApplicationRecord
  before_save :capitalize_title

  private

  def capitalize_title
    self.title = title.capitalize
  end
end
```

---

### **Validations**

Model-level validations သုံးပြီး data integrity ကို secure လုပ်ပါတယ်။

**ဥပမာ:**
```ruby
class Book < ApplicationRecord
  validates :title, presence: true, uniqueness: true
  validates :description, length: { minimum: 10 }
end
```

---

### **Conclusion**

Active Record သည် Ruby on Rails application အတွက် database operations, data relationships, validations, နှင့် schema management များကို လွယ်ကူစေတဲ့ powerful tool ဖြစ်ပါတယ်။ Rails ရဲ့ **Convention over Configuration** concept ကို လိုက်နာပြီး database နှင့် seamless integration ကို အသုံးပြုနိုင်ပါသည်။