### **Ruby on Rails - Directory Structure**

Ruby on Rails (Rails) တွင် application တစ်ခု ဖန်တီးလိုက်ပါက, အကြောင်းအရာများကို အစဉ်အလာအတိုင်း အလိုအလျောက် directory structure များမှာ ထည့်သွင်းပေးပါသည်။ အဲဒါကြောင့် Rails ၏ directory structure ကို သိရှိခြင်းဟာ project ကို အကောင်းဆုံး စီမံခန့်ခွဲဖို့ အရေးကြီးပါတယ်။

Rails application ရဲ့ default directory structure သည် သင့်ကို MVC (Model-View-Controller) architectural pattern အတိုင်း အဆင်ပြေစွာ ယူသုံးနိုင်စေပါသည်။ အောက်တွင် **Ruby on Rails directory structure** ၏ အဓိကအချက်များကို ရှင်းလင်းပေးပါမယ်။

---

### **1. Rails Directory Structure**

Ruby on Rails application တစ်ခု ဖန်တီးတဲ့အခါ **app**, **config**, **db**, **public**, **test**, **log**, **tmp** စသည့် directories များကို automatic ပေါ်လာပါတယ်။ အောက်မှာ အဓိက directory များကို ခွဲခြားပြီး ရှင်းပြထားပါတယ်။

#### **1.1. `app/` Directory**

`app/` directory သည် Rails application ၏ **business logic** နှင့် **view rendering** ကို ထိန်းချုပ်သည့် အဓိက directory ဖြစ်ပါသည်။ ဒီမှာ **Model**, **View**, **Controller** စသည့် files များရှိပါသည်။

- **`app/controllers/`**: Controller files များကို အတည်ပြုသည့် directory ဖြစ်သည်။ Controller သည် user requests များကို handle လုပ်ပြီး, models နှင့် views နှင့်ချိတ်ဆက်ပြီး response များပေးပါသည်။
  - **Example**: `users_controller.rb`

- **`app/models/`**: Models များကို သိမ်းဆည်းသည့် directory ဖြစ်သည်။ Model files တွင် database interaction logic နှင့် data validation logic များ ပါဝင်သည်။
  - **Example**: `user.rb`

- **`app/views/`**: View files များကို သိမ်းဆည်းသည့် directory ဖြစ်သည်။ View တွင် **HTML** နှင့် **embedded Ruby** (ERB) code များ ပါဝင်ပြီး, User interface (UI) ကို ဖော်ပြပါတယ်။
  - **Example**: `users/show.html.erb`

- **`app/helpers/`**: Helper files များကို သိမ်းဆည်းသည့် directory ဖြစ်သည်။ View ကို generate လုပ်ရာတွင် reusable code များကို အကောင်အထည်ဖော်ရန် helper functions များပါဝင်ပါတယ်။

- **`app/assets/`**: **CSS**, **JavaScript**, **images** စသည့် static files များကို သိမ်းဆည်းရာကနေ, **asset pipeline** ကိုအသုံးပြု၍ စီမံခန့်ခွဲရပါတယ်။
  - **Example**: `application.css`, `application.js`

#### **1.2. `config/` Directory**

`config/` directory သည် Rails application ၏ **configuration** files များကို သိမ်းဆည်းထားသော directory ဖြစ်ပါသည်။

- **`config/routes.rb`**: ဒီ file တွင် application ရဲ့ **routes** များကို ဖော်ပြထားသည်။ User requests များကို မည်သည့် controller နှင့် action နှင့် ဆက်သွယ်မလဲဆိုတာကို ဆုံးဖြတ်သည်။
  - **Example**: `resources :users`

- **`config/database.yml`**: Database connection settings များကို သိမ်းဆည်းထားသော file ဖြစ်သည်။ MySQL, PostgreSQL, SQLite3 စတဲ့ database systems များကို configure လုပ်နိုင်ပါသည်။

- **`config/environments/`**: Development, production, test environment များအတွက် configuration files များ ပါဝင်သည်။
  - **Example**: `development.rb`, `production.rb`

#### **1.3. `db/` Directory**

`db/` directory သည် Rails application ၏ **database-related** files များကို သိမ်းဆည်းထားသော directory ဖြစ်ပါသည်။

- **`db/migrate/`**: **Database migration files** များကို ထိန်းသိမ်းထားသည်။ Rails များတွင် database schema အပြောင်းအလဲများကို **migrations** များဖြင့် ပြုလုပ်သည်။
  - **Example**: `20231217120000_create_users.rb`

- **`db/seeds.rb`**: Application ၏ database ကို initial data များဖြင့် populate လုပ်ရန်အတွက် **seeds file** ပါဝင်သည်။

#### **1.4. `public/` Directory**

`public/` directory သည် **static files** များကို သိမ်းဆည်းထားသော directory ဖြစ်သည်။ Rails application ကို run လုပ်သောအခါ, static files (images, JavaScript, CSS) များအား **public** directory မှာ ရရှိနိုင်ပါသည်။

- **Example**: `public/index.html`, `public/images/logo.png`

#### **1.5. `test/` Directory**

`test/` directory သည် **testing** files များကို သိမ်းဆည်းထားသော directory ဖြစ်သည်။ Rails application များ၏ **unit tests**, **integration tests**, **functional tests** များကို ဒီ directory မှာ ရေးသားနိုင်ပါတယ်။

- **`test/controllers/`**: Controller tests များကို သိမ်းဆည်းထားသည်။
  - **Example**: `users_controller_test.rb`

- **`test/models/`**: Model tests များကို သိမ်းဆည်းထားသည်။
  - **Example**: `user_test.rb`

#### **1.6. `log/` Directory**

`log/` directory သည် application ၏ **log files** များကို သိမ်းဆည်းထားသော directory ဖြစ်သည်။ ဒီမှာ **development.log**, **production.log** စသည့် log files များ ပါဝင်ပါတယ်။

- **Example**: `development.log`, `production.log`

#### **1.7. `tmp/` Directory**

`tmp/` directory သည် **temporary files** များကို သိမ်းဆည်းထားသည်။ Cache, session data, process-related temporary files များကို ဒီ directory မှာ သိမ်းထားပါသည်။

- **Example**: `tmp/cache`, `tmp/sessions`

#### **1.8. `vendor/` Directory**

`vendor/` directory သည် third-party libraries များကို သိမ်းဆည်းထားသော directory ဖြစ်သည်။ Rails application တွင် **gems** များ၊ **plugins** များကို **vendor** directory ထဲမှာ သိမ်းနိုင်ပါသည်။

---

### **2. Summary of Rails Directory Structure**

Ruby on Rails application တွင် directory structure ကို အသုံးပြုခြင်းအားဖြင့် application development ကို အလွယ်တကူ စီမံခန့်ခွဲနိုင်ပါသည်။ အခြေခံထားသည့် **MVC** architecture နှင့် နည်းလမ်းများအပေါ် အခြေခံပြီး, application ၏ လုပ်ငန်းများကို အဆင်ပြေစွာ စီမံနိုင်ပါသည်။ အဓိက directory များမှာ `app/`, `config/`, `db/`, `public/`, `test/`, `log/`, `tmp/`, `vendor/` တို့ပါဝင်သည်။

- **`app/`**: Model, View, Controller (MVC logic)
- **`config/`**: Configuration files
- **`db/`**: Database-related files
- **`public/`**: Static files
- **`test/`**: Testing files
- **`log/`**: Log files
- **`tmp/`**: Temporary files
- **`vendor/`**: Third-party libraries

Rails ၏ **convention over configuration** principle အရ, Rails developers များသည် လုပ်ဆောင်ရမည့် tasks များကို directory structure ကို အခြေခံပြီး, အလွယ်တကူ ပြီးမြောက်စေပါသည်။