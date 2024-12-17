### **Ruby Web Applications - CGI Programming**

CGI (Common Gateway Interface) သည် Web servers နှင့် external applications (သို့မဟုတ် scripts) များအကြားအချိတ်အဆက်လုပ်ငန်းဆောင်ရန် အသုံးပြုသော protocol တစ်ခုဖြစ်သည်။ Ruby ကို CGI programming တွင် အသုံးပြု၍ Web applications များကို ဆောက်တည်နိုင်သည်။ Ruby နှင့် CGI ကို အသုံးပြုပြီး Web server များအတွက် dynamic content များကို generate လုပ်နိုင်ပါတယ်။

---

### **1. CGI Programming အကြောင်း**

CGI programming သည် **Web Server** နှင့် **Server-side Scripts** ကြား communication ကို စီမံခန့်ခွဲပေးသည့် protocol ဖြစ်ပြီး၊ ရှုပ်ထွေးသော dynamic content များကို ထုတ်လုပ်ရန် အသုံးပြုသည်။ Ruby language သည် CGI scripts တွေအတွက် တစ်ခုသော programming language တစ်ခုအဖြစ် အလွယ်တကူ အသုံးပြုနိုင်ပါသည်။

---

### **2. Ruby CGI Programming Setup**

Ruby CGI programming ကို စတင်ရန် **CGI module** ကို `require` ဖြင့် load ပြီး CGI scripts တွေကို run ခြင်းဖြင့် Web server မှ request များကို process လုပ်နိုင်ပါတယ်။

#### **2.1. CGI module Installation**
Ruby မှာ CGI module ကို အခမဲ့တင်သွင်းပေးထားပြီး, Ruby installation များတွင် already installed ဖြစ်နေလိမ့်မည်။

Ruby CGI program တွေကိုသုံးရန် `cgi` module ကို import လုပ်ရန်လိုအပ်ပါသည်။

```ruby
require 'cgi'
```

---

### **3. Basic CGI Script Example**

Ruby CGI scripts ကို run ပြုလုပ်ရန် Web server ကို configure လုပ်ပြီး script ကို execute လုပ်ရန်လိုပါတယ်။ Ruby CGI script တွေမှာ `CGI` module က အဓိကအသုံးပြုသော method များဖြစ်ပြီး input data ကို HTTP request မှသွင်းပြီး response data ကို server မှပြန်ပေးသည်။

```ruby
#!/usr/bin/ruby

require 'cgi'

# CGI object
cgi = CGI.new

# Send HTTP header
cgi.out("type" => "text/html") do
  # Response body
  "<html><body><h1>Hello, Ruby CGI!</h1></body></html>"
end
```

**Explanation:**
- **`CGI.new`**: `CGI` object တစ်ခုကို initialize လုပ်ပြီး HTTP request data ကို process လုပ်နိုင်ပါတယ်။
- **`cgi.out`**: HTTP header နှင့် content type ကို specify လုပ်ပြီး, HTML response body ကို return လုပ်ပါတယ်။
- **Output**: Web browser မှာ **`Hello, Ruby CGI!`** ဆိုတဲ့ message ကို output ပြသမည်။

---

### **4. Sending and Receiving Form Data**

Web applications တွင် user input ကို form များမှ ရယူရန် CGI programming ကိုအသုံးပြုနိုင်ပါတယ်။ Ruby CGI သည် form data ကို `CGI` object မှတစ်ဆင့် ရယူနိုင်ပါတယ်။

#### **4.1 HTML Form Example**

```html
<form action="/cgi-bin/ruby_cgi_script.rb" method="post">
  Name: <input type="text" name="name"><br>
  Age: <input type="text" name="age"><br>
  <input type="submit" value="Submit">
</form>
```

#### **4.2 Ruby CGI Script Example for Receiving Form Data**

```ruby
#!/usr/bin/ruby

require 'cgi'

cgi = CGI.new

# Get form data
name = cgi['name']
age = cgi['age']

# Send HTTP header
cgi.out("type" => "text/html") do
  # Response body
  "<html><body><h1>Hello, #{name}!</h1><p>You are #{age} years old.</p></body></html>"
end
```

**Explanation:**
- **`cgi['name']`** နှင့် **`cgi['age']`** က form မှ user input values တွေကို `CGI` object မှတစ်ဆင့် ရယူပါသည်။
- Web browser တွင် `Name` နှင့် `Age` field တွေကို user က fill-in ပြီး submit လုပ်လိုက်ရင်၊ **"Hello, [name]"** နှင့် **"You are [age] years old."** ဆိုသော response ကို display ပြပါလိမ့်မယ်။

---

### **5. Working with CGI Environment Variables**

CGI programming မှာ environment variables တွေကိုလည်း အသုံးပြုနိုင်ပါတယ်။ Ruby CGI မှာ **`ENV`** object သုံးပြီး Web server မှပေးထားတဲ့ environment variables များကို access ပြုလုပ်နိုင်ပါသည်။

#### **5.1. Example of Accessing Environment Variables**

```ruby
#!/usr/bin/ruby

require 'cgi'

cgi = CGI.new

# Get environment variables
server_software = ENV['SERVER_SOFTWARE']
remote_addr = ENV['REMOTE_ADDR']

# Send HTTP header
cgi.out("type" => "text/html") do
  # Response body
  "<html><body>
    <h1>CGI Environment Variables</h1>
    <p>Server Software: #{server_software}</p>
    <p>Client IP Address: #{remote_addr}</p>
  </body></html>"
end
```

**Explanation:**
- **`ENV['SERVER_SOFTWARE']`** နှင့် **`ENV['REMOTE_ADDR']`** က server software information နှင့် client IP address ကို access လုပ်နိုင်ပါတယ်။

---

### **6. Error Handling in Ruby CGI**

CGI programming တွင် error handling အရေးကြီးပါတယ်။ CGI script များမှာ Ruby’s **`begin-rescue`** block ကို အသုံးပြု၍ error handling ပြုလုပ်နိုင်ပါတယ်။

#### **6.1. Error Handling Example**

```ruby
#!/usr/bin/ruby

require 'cgi'

cgi = CGI.new

begin
  # Simulate an error
  result = 10 / 0
rescue ZeroDivisionError => e
  # Handle the error
  cgi.out("type" => "text/html") do
    "<html><body><h1>Error: #{e.message}</h1></body></html>"
  end
end
```

**Explanation:**
- **`ZeroDivisionError`** က error type ဖြစ်ပြီး, error ဖြစ်နေတဲ့ code ကို **`rescue`** block က catch လုပ်ပြီး user ကို error message ကို output ပြပါလိမ့်မယ်။

---

### **7. CGI Script Deployment**

Ruby CGI scripts ကို **Web server** မှာ run ချင်လျှင်, အောက်ပါလုပ်ဆောင်ချက်များကိုလိုက်နာပါ။

1. **Web Server Installation**: Apache HTTP server သို့မဟုတ် Nginx ကို install လုပ်ထားရပါမည်။
2. **CGI Configuration**: Web server မှာ **CGI** configuration ကို enable လုပ်ရပါမည်။

#### **Apache Web Server Configuration Example**
- **`/etc/httpd/conf/httpd.conf`** file မှာ CGI enable လုပ်ရန်:

```bash
<Directory "/path/to/your/cgi-bin">
  Options +ExecCGI
  AddHandler cgi-script .cgi .pl .rb
</Directory>
```

- **CGI Scripts Directory**: CGI scripts တွေကို `cgi-bin` directory ထဲမှာ သိမ်းဆည်းထားရပါသည်။

---

Ruby CGI programming သည် Web development များတွင် **dynamic web pages** ရရှိရန် **server-side scripting** ရေးသားရန် အလွန်အရေးကြီးသော tool တစ်ခုဖြစ်သည်။ Ruby နဲ့ CGI ကိုအသုံးပြုခြင်းက server နှင့် client အကြား request-response cycle ကို အလွယ်တကူ process လုပ်နိုင်ပြီး user input ကိုလည်း မတူညီသော format တွေနဲ့ ပြန်လည် output ပြုလုပ်နိုင်ပါတယ်။

CGI programming ကို အသုံးပြုဖို့ Ruby code များကို **`CGI.new`** နှင့် **`cgi.out`** method များကို အသုံးပြုပြီး, form data, environment variables နှင့် error handling စတာတွေလည်း လွယ်ကူစွာ လုပ်ဆောင်နိုင်ပါတယ်။