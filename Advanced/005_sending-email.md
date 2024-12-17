### **Sending Email using Ruby - SMTP**

Ruby မှာ email ပို့ရန် **SMTP (Simple Mail Transfer Protocol)** ကို အသုံးပြုနိုင်ပါတယ်။ Ruby မှာ **`net/smtp`** module ကို အသုံးပြုပြီး SMTP server မှတဆင့် email ပို့နိုင်ပါတယ်။ SMTP သည် email servers နှစ်ခုကြား email messages များကို လွှဲပြောင်းပို့ရန် အသုံးပြုသော protocol ဖြစ်သည်။

---

### **1. Ruby SMTP Setup**

Ruby မှာ SMTP server တွေနဲ့ communication ပြုလုပ်ရန် **`net/smtp`** gem ကို အသုံးပြုနိုင်ပါသည်။ ဒီ library သည် Ruby မှာ SMTP protocol ကို အသုံးပြု၍ email များကို ပို့ပေးနိုင်တဲ့ built-in functionality ရှိပါတယ်။

---

### **2. Ruby SMTP Example**

Ruby သုံးပြီး email ပို့ရန် အောက်ပါ နမူနာကို ကြည့်ပါ။

```ruby
require 'net/smtp'

# Email content
message = <<~MESSAGE_END
  From: sender@example.com
  To: recipient@example.com
  Subject: Hello from Ruby!

  This is a test email sent from Ruby using SMTP.
MESSAGE_END

# SMTP server details
smtp_server = 'smtp.example.com'  # SMTP server address
smtp_port = 587  # SMTP port (587 for TLS, 25 for non-secure)
smtp_domain = 'example.com'  # SMTP domain
smtp_user = 'sender@example.com'  # Sender's email address
smtp_password = 'password'  # Sender's email password

# Send email
Net::SMTP.start(smtp_server, smtp_port, smtp_domain, smtp_user, smtp_password, :login) do |smtp|
  smtp.send_message message, 'sender@example.com', 'recipient@example.com'
  puts "Email sent successfully!"
end
```

---

### **3. Explanation**

1. **Email Message:**
   - `message = <<~MESSAGE_END ... MESSAGE_END` ဆိုတာက email ရဲ့ content ဖြစ်ပြီး, `From`, `To`, `Subject` headers များနဲ့ တစ်နေရာတည်းမှာ email message ကို ဖော်ပြထားပါတယ်။
   - **`From:`** ပို့သူအီးမေးလ်လိပ်စာ။
   - **`To:`** လက်ခံသူအီးမေးလ်လိပ်စာ။
   - **`Subject:`** email ရဲ့ ခေါင်းစဉ်။
   
2. **SMTP Server Configuration:**
   - `smtp_server = 'smtp.example.com'` ဆိုတာက SMTP server ရဲ့ address ဖြစ်ပြီး, SMTP server တစ်ခုမှ email ပို့ဖို့ သတ်မှတ်ထားတဲ့ server address ကို ပြသထားပါတယ်။
   - `smtp_port = 587` သည် port number ဖြစ်ပြီး, TLS encryption ကို အသုံးပြုရန် **587** port ကိုအသုံးပြုပါသည်။ ပုံမှန် SMTP server ၏ default port number သည် **25** ဖြစ်သော်လည်း, security purposes အတွက် **587** သည် common choice ဖြစ်ပါသည်။
   - `smtp_user` နှင့် `smtp_password` က user credentials ဖြစ်ပြီး, ထို email account ၏ username နှင့် password ကိုသတ်မှတ်ထားပါသည်။

3. **Sending the Email:**
   - `Net::SMTP.start` method သည် SMTP server နှင့် connection တစ်ခုဖွင့်ပြီး, အီးမေးလ်ကိုပို့သော function ဖြစ်ပါသည်။
   - `smtp.send_message` က email message ကို ပို့သူနဲ့ လက်ခံသူအီးမေးလ်လိပ်စာကို အသုံးပြုပြီး ပို့ပေးပါသည်။

---

### **4. TLS (Transport Layer Security) / SSL Encryption**

TLS သို့မဟုတ် SSL encryption များကို အသုံးပြုပါက ပိုပြီး secure ဖြစ်သည်။ Ruby မှာ TLS/SSL ကို automatically handle လုပ်နိုင်ပါတယ်။ Ruby `net/smtp` library သည် **`starttls`** ကို support လုပ်ပြီး, encrypted connection များကို use လုပ်နိုင်ပါတယ်။

#### **4.1. TLS Example**

```ruby
require 'net/smtp'

message = <<~MESSAGE_END
  From: sender@example.com
  To: recipient@example.com
  Subject: Secure Email from Ruby!

  This is a test email sent from Ruby using SMTP with TLS encryption.
MESSAGE_END

smtp_server = 'smtp.example.com'
smtp_port = 587  # TLS port
smtp_user = 'sender@example.com'
smtp_password = 'password'

# Send email with TLS encryption
Net::SMTP.start(smtp_server, smtp_port, 'example.com', smtp_user, smtp_password, :login) do |smtp|
  smtp.enable_starttls  # Enable TLS encryption
  smtp.send_message message, 'sender@example.com', 'recipient@example.com'
  puts "Secure email sent successfully!"
end
```

**Explanation:**
- **`smtp.enable_starttls`** သည် TLS encryption ကို enable လုပ်ရန် command ဖြစ်ပါသည်။ email ကို encrypted connection ပေါ်မှာပဲပို့လိမ့်မည်။

---

### **5. Common SMTP Providers**

Ruby နှင့် SMTP email ပို့ခြင်းကို မိမိ၏ email provider အပေါ်မှအခြေခံပြီး configure ပြုလုပ်နိုင်ပါတယ်။ အချို့သော common SMTP servers များမှာ:

- **Gmail (smtp.gmail.com)**
  - SMTP Server: `smtp.gmail.com`
  - Port: `587` (TLS), `465` (SSL)
  - Login: Gmail username (e.g., `yourusername@gmail.com`)
  - Password: Gmail password (or App Password if 2FA enabled)

- **Yahoo (smtp.mail.yahoo.com)**
  - SMTP Server: `smtp.mail.yahoo.com`
  - Port: `587` (TLS), `465` (SSL)
  - Login: Yahoo email address (e.g., `yourusername@yahoo.com`)
  - Password: Yahoo password

- **Outlook (smtp-mail.outlook.com)**
  - SMTP Server: `smtp-mail.outlook.com`
  - Port: `587` (TLS)
  - Login: Outlook email address (e.g., `yourusername@outlook.com`)
  - Password: Outlook password

---

### **6. Handling Errors in SMTP**

SMTP operations မှာ အမှားတက်နိုင်ပါသည်။ Ruby မှာ **`begin-rescue`** block ကို error handling အတွက်အသုံးပြုနိုင်ပါတယ်။

#### **6.1. SMTP Error Handling Example**

```ruby
require 'net/smtp'

begin
  message = <<~MESSAGE_END
    From: sender@example.com
    To: recipient@example.com
    Subject: Email with Error Handling

    This is a test email sent from Ruby with error handling.
  MESSAGE_END

  smtp_server = 'smtp.example.com'
  smtp_user = 'sender@example.com'
  smtp_password = 'password'

  # Send email
  Net::SMTP.start(smtp_server, 587, 'example.com', smtp_user, smtp_password, :login) do |smtp|
    smtp.send_message message, 'sender@example.com', 'recipient@example.com'
  end

  puts "Email sent successfully!"
rescue Net::SMTPAuthenticationError => e
  puts "Authentication failed: #{e.message}"
rescue Net::SMTPServerBusy => e
  puts "SMTP Server is busy: #{e.message}"
rescue StandardError => e
  puts "An error occurred: #{e.message}"
end
```

**Explanation:**
- **`Net::SMTPAuthenticationError`**: SMTP authentication error ဖြစ်ပါက တက်တဲ့ exception ကို handle လုပ်ပါတယ်။
- **`Net::SMTPServerBusy`**: SMTP server ပြဿနာရှိနေပါက အမှားကို handle လုပ်ပါသည်။
- **`StandardError`**: အခြားအမှားများကို handle လုပ်သော generic error handler ဖြစ်ပါသည်။

---

Ruby မှာ SMTP သုံးပြီး email ပို့ခြင်းသည် အလွန်လွယ်ကူပါသည်။ **`net/smtp`** library သည် email များကို SMTP server များမှတဆင့် ပို့ပေးရန် အရေးကြီးသော tools များကိုပေးထားသည်။ **TLS/SSL encryption** များကိုအသုံးပြုခြင်းဖြင့် security ကို မြှင့်တင်နိုင်ပြီး, email ပို့ခြင်းကို secure စွာလုပ်ဆောင်နိုင်ပါတယ်။