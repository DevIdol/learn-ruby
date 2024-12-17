### **Ruby on Rails - Installation**

Ruby on Rails ကို သင့်ကွန်ပျူတာတွင် install လုပ်ရန်အတွက် အောက်ပါအဆင့်များကို လိုက်နာနိုင်ပါတယ်။ Rails ကို install လုပ်ရန်မှာ **Ruby** programming language ကို အရင်ဆုံး install လုပ်ရမယ်၊ ပြီးနောက် **Rails** ကို install လုပ်ပြီး၊ လေ့လာမှုများစွာကို ရနိုင်ပါသည်။

---

### **1. Ruby Installation**

Rails ကို install လုပ်ရန်အတွက် အရင်ဆုံး **Ruby** ကို သင့် system မှာ install လုပ်ရပါမယ်။ Ruby သည် Ruby on Rails နေရာတွင် အခြေခံ programming language ဖြစ်သည်။

#### **1.1. Windows အတွက် Ruby Install လုပ်ခြင်း**

Windows တွင် Ruby ကို install လုပ်ရန် **RubyInstaller** ကို အသုံးပြုနိုင်ပါသည်။

1. [RubyInstaller](https://rubyinstaller.org/) website သို့သွားပါ။
2. Windows အတွက် **RubyInstaller** version ကို download လုပ်ပါ (32-bit/64-bit အတွက် အထူးပြု version များ ရွေးချယ်နိုင်သည်)။
3. Installer ကို run လုပ်ပြီး **Ruby** ကို install လုပ်ပါ။ `Add Ruby executables to your PATH` option ကို အတည်ပြုပါ။
4. Command Prompt တွင် `ruby -v` ဆိုပြီး Ruby version ကို စစ်ဆေးပါ။ အကယ်၍ Ruby ကို အောင်မြင်စွာ install လုပ်ထားရင် Ruby version ပြပါလိမ့်မယ်။

---

#### **1.2. macOS အတွက် Ruby Install လုပ်ခြင်း**

macOS တွင် Ruby သည် အဆင့်မြင့် version များကို **Homebrew** package manager ကနေ install လုပ်နိုင်ပါတယ်။

1. **Homebrew** ကို install လုပ်ရန် Terminal မှာ အောက်ပါ command ကို ရိုက်ပါ။

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. Homebrew ကို install လုပ်ပြီးနောက်, Ruby ကို install လုပ်ရန် အောက်ပါ command ကို အသုံးပြုပါ။

   ```bash
   brew install ruby
   ```

3. Ruby ကို install လုပ်ပြီးပါက, version ကို စစ်ဆေးရန် `ruby -v` ကို terminal မှာ ရိုက်ပါ။

---

#### **1.3. Linux (Ubuntu) အတွက် Ruby Install လုပ်ခြင်း**

Linux Ubuntu တွင် Ruby ကို **APT** package manager ကနေ အလွယ်တကူ install လုပ်နိုင်ပါတယ်။

1. Terminal မှာ အောက်ပါ command ကို အသုံးပြုပါ။

   ```bash
   sudo apt update
   sudo apt install ruby-full
   ```

2. Ruby ကို install လုပ်ပြီးရင်, version ကို စစ်ဆေးရန် `ruby -v` ရိုက်ပါ။

---

### **2. Rails Installation**

Ruby ကို အောင်မြင်စွာ install လုပ်ပြီးပါက Rails ကို install လုပ်ခြင်းအဆင့်ကို ဆက်လုပ်နိုင်ပါပြီ။

#### **2.1. Install Rails with gem**

Ruby on Rails ကို **gem** (Ruby package manager) ကို အသုံးပြု၍ install လုပ်နိုင်ပါသည်။ Terminal (Command Prompt) မှာ အောက်ပါ command ကို ရိုက်ပါ။

```bash
gem install rails
```

ထိုအခါ Rails ကို install လုပ်ခြင်းမပြီးစီးပါက, **Rails version** ကို စစ်ဆေးရန် command ကို ရိုက်ပါ။

```bash
rails -v
```

Rails ကို အောင်မြင်စွာ install လုပ်လျှင် Rails version ကို ပြပါလိမ့်မယ်။

---

### **3. Database Installation**

Rails application များတွင် **database** ကိုအသုံးပြုရပါမယ်။ Rails ၏ default database သည် **SQLite3** ဖြစ်ပါသည်။ သို့သော် PostgreSQL, MySQL အစရှိသည့် database များကိုလည်း အသုံးပြုနိုင်ပါသည်။

#### **3.1. Install SQLite3**

SQLite3 သည် Rails ၏ default database ဖြစ်ပြီး၊ Rails ၏ အများဆုံး tutorial များတွင် အသုံးပြုပါသည်။

- **Windows**: SQLite3 ကို [SQLite website](https://www.sqlite.org/download.html) မှာ download လုပ်နိုင်ပါသည်။
- **macOS**: macOS တွင် **Homebrew** ကနေ SQLite3 ကို install လုပ်နိုင်ပါသည်။

   ```bash
   brew install sqlite
   ```

- **Linux**: Ubuntu တွင် SQLite3 ကို APT package manager ဖြင့် install လုပ်နိုင်ပါတယ်။

   ```bash
   sudo apt install sqlite3 libsqlite3-dev
   ```

---

### **4. Creating a New Rails Application**

Rails ကို install လုပ်ပြီးပြီးနောက်, Rails application တစ်ခု ဖန်တီးရန်အတွက် `rails new` command ကို အသုံးပြုနိုင်ပါတယ်။

#### **4.1. New Rails Application Creation**

1. Terminal မှာ အောက်ပါ command ကို ရိုက်ပါ။ `myapp` ဆိုတဲ့ app name ကို သင်လိုချင်သည့်အတိုင်းပြောင်းနိုင်ပါတယ်။

   ```bash
   rails new myapp
   ```

2. **Rails app** ကို ဖန်တီးပြီးပါက, အဲ့ဒီ folder ထဲသို့ ဝင်ပါ။

   ```bash
   cd myapp
   ```

---

### **5. Running the Rails Server**

Rails application တစ်ခုဖန်တီးပြီးပါက, Rails server ကို run လုပ်ခြင်းဖြင့် application ကို browser မှာ ပေါ်လာစေပါသည်။

#### **5.1. Start the Rails Server**

1. Rails server ကို အောက်ပါ command ဖြင့် run ပါ။

   ```bash
   rails server
   ```

2. Server run ဖြစ်ပါက, **http://localhost:3000** ကို browser မှာ ဖွင့်ပြီး application ကို အဆင်ပြေစွာ ကြည့်နိုင်ပါသည်။

---

### **6. Troubleshooting and Common Issues**

Ruby on Rails ကို install လုပ်ရာတွင် အခက်အခဲများရှိပါက, အောက်ပါအဆင့်များကို စစ်ဆေးပါ။

1. **Ruby version** မှားနေခြင်း: Rails နှင့် Ruby version များသည် အသုံးပြုနိုင်သော version များရှိပါသည်။ အကယ်၍ version မကိုက်ညီပါက, version ကို ပြောင်းရန် **RVM** (Ruby Version Manager) သို့မဟုတ် **rbenv** ကို အသုံးပြုပါ။

2. **Dependencies** မလိုအပ်သော package များ ရှိခြင်း: `bundle install` သည် application ရဲ့ dependencies များကို install လုပ်ပေးပါသည်။

   ```bash
   bundle install
   ```

3. **Database connection**: Database ကို အတည်ပြုရန် command prompt တွင် `rails db:create` ကို run လုပ်ပါ။

---

### **Conclusion**

Ruby on Rails ကို install လုပ်ရတာက အလွန်လွယ်ကူပြီး, Web development မှာ Rails ကိုအသုံးပြုရမှာ အရမ်းအဆင်ပြေပါတယ်။ Rails ကို install လုပ်ပြီးနောက်, Rails application ဖန်တီးခြင်း, database configuration များ, server run စတာတွေကို အလွယ်တကူ လုပ်နိုင်ပါပြီ။ Rails အနေဖြင့် rapid development, clean code structure, နှင့် scalability ရှိတဲ့ framework တစ်ခု ဖြစ်ပါတယ်။