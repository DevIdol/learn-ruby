### **Ruby - Date & Time**

Ruby မှာ **Date** နဲ့ **Time** ကို Handle လုပ်ဖို့အတွက် Built-in Libraries ရှိပါတယ်။  
အချိန်၊ နေ့ရက်တွေကို သတ်မှတ်၊ ပြန်လည်ရယူ၊ Manipulate နဲ့ Format လုပ်နိုင်ပါတယ်။  

---

## **1. Date & Time Classes**

Ruby မှာ Date နဲ့ Time ကို Handle လုပ်တဲ့ Classes အထွေထွေ ၂ မျိုးရှိတယ်။
- **`Date` Class**: နေ့ရက် (Date) ကို Manage လုပ်ဖို့။
- **`Time` Class**: အချိန် (Time) ကို Manage လုပ်ဖို့။
- **`DateTime` Class**: Date နဲ့ Time နှစ်ခုလုံး Handle လုပ်နိုင်တဲ့ Class။

---

## **2. Time Class**

### **2.1 Current Time**
Ruby မှာ **`Time.now`** နဲ့ Current Time ကို ရယူနိုင်ပါတယ်။
```ruby
current_time = Time.now
puts current_time
# Output: 2024-12-17 15:30:00 +0000 (Example)
```

---

### **2.2 Time Object ထဲက Values ကို Access လုပ်ခြင်း**
```ruby
current_time = Time.now
puts current_time.year   # 2024
puts current_time.month  # 12
puts current_time.day    # 17
puts current_time.hour   # 15
puts current_time.min    # 30
puts current_time.sec    # 0
```

---

### **2.3 Custom Time Object**
**`Time.new`** နဲ့ ကိုယ်လိုချင်တဲ့ Time Object ကို ဖန်တီးနိုင်ပါတယ်။
```ruby
custom_time = Time.new(2023, 12, 25, 10, 30, 0)
puts custom_time
# Output: 2023-12-25 10:30:00 +0000
```

---

### **2.4 Time Arithmetic**
Time Object တွေကို Plus (+) နဲ့ Minus (-) လုပ်ပြီး Calculation လုပ်နိုင်တယ်။
```ruby
time_now = Time.now
time_future = time_now + (60 * 60 * 24)  # Add 1 day
time_past = time_now - (60 * 60 * 24)    # Subtract 1 day

puts time_future
puts time_past
```

---

### **2.5 Comparing Times**
Time Object တွေကို Compare လုပ်လို့ရတယ်။
```ruby
time1 = Time.new(2023, 12, 25)
time2 = Time.new(2024, 12, 25)

puts time1 < time2  # true
puts time1 == time2 # false
puts time1 > time2  # false
```

---

## **3. Date Class**

### **3.1 Requiring the Date Library**
Ruby မှာ **Date** ကို အသုံးပြုဖို့ **`require 'date'`** လိုအပ်ပါတယ်။
```ruby
require 'date'

# Current date
current_date = Date.today
puts current_date
# Output: 2024-12-17 (Example)
```

---

### **3.2 Custom Date Object**
```ruby
require 'date'

custom_date = Date.new(2023, 12, 25)
puts custom_date
# Output: 2023-12-25
```

---

### **3.3 Date Arithmetic**
```ruby
require 'date'

date_now = Date.today
date_future = date_now + 10  # Add 10 days
date_past = date_now - 10    # Subtract 10 days

puts date_future
puts date_past
```

---

### **3.4 Accessing Date Components**
```ruby
require 'date'

current_date = Date.today
puts current_date.year   # 2024
puts current_date.month  # 12
puts current_date.day    # 17
```

---

## **4. DateTime Class**

Date နဲ့ Time နှစ်ခုလုံးကို Handle လုပ်ဖို့ **`DateTime`** ကို အသုံးပြုနိုင်ပါတယ်။  
**`require 'date'`** လိုအပ်ပါတယ်။
```ruby
require 'date'

datetime_now = DateTime.now
puts datetime_now
# Output: 2024-12-17T15:30:00+00:00

custom_datetime = DateTime.new(2023, 12, 25, 10, 30, 0)
puts custom_datetime
# Output: 2023-12-25T10:30:00+00:00
```

---

## **5. Formatting Dates and Times**

Date နဲ့ Time ကို ကိုယ်လိုချင်တဲ့ Format နဲ့ ပြောင်းဖို့ **`strftime`** ကို အသုံးပြုနိုင်တယ်။

### **5.1 Common Format Codes**
| Code | Description       | Example      |
|------|-------------------|--------------|
| `%Y` | Year (4 digits)   | `2024`       |
| `%m` | Month (2 digits)  | `12`         |
| `%d` | Day (2 digits)    | `17`         |
| `%H` | Hour (24-hour)    | `15`         |
| `%M` | Minutes           | `30`         |
| `%S` | Seconds           | `00`         |
| `%p` | AM/PM             | `PM`         |

### **5.2 Example**
```ruby
time_now = Time.now
formatted_time = time_now.strftime("%Y-%m-%d %H:%M:%S")
puts formatted_time
# Output: 2024-12-17 15:30:00
```

---

## **6. Parsing Dates and Times**

### **6.1 Using `Time.parse`**
```ruby
require 'time'

parsed_time = Time.parse("2024-12-17 15:30:00")
puts parsed_time
# Output: 2024-12-17 15:30:00 +0000
```

### **6.2 Using `Date.parse`**
```ruby
require 'date'

parsed_date = Date.parse("2024-12-17")
puts parsed_date
# Output: 2024-12-17
```

---

## **7. Time Zones**

Ruby မှာ Time Zones ကို Handle လုပ်ဖို့ **`ActiveSupport::TimeZone`** သို့မဟုတ် Third-party Gems တွေလိုအပ်နိုင်ပါတယ်။

```ruby
require 'time'

utc_time = Time.now.utc
puts utc_time
# Output: 2024-12-17 15:30:00 UTC
```

---

## **8. Summary Table**

| **Functionality**       | **Code**                                  | **Example Output**              |
|-------------------------|------------------------------------------|---------------------------------|
| Current Time            | `Time.now`                              | `2024-12-17 15:30:00 +0000`    |
| Current Date            | `Date.today`                            | `2024-12-17`                   |
| Custom Time             | `Time.new(2023, 12, 25, 10, 30)`         | `2023-12-25 10:30:00 +0000`    |
| Custom Date             | `Date.new(2023, 12, 25)`                 | `2023-12-25`                   |
| Add Days to Date        | `Date.today + 10`                       | `2024-12-27`                   |
| Formatting              | `Time.now.strftime("%Y-%m-%d")`         | `2024-12-17`                   |
| Parsing Date            | `Date.parse("2024-12-17")`              | `2024-12-17`                   |

---

**ရိုးရှင်းပြီး Flexible ဖြစ်တဲ့ Ruby ရဲ့ Date နဲ့ Time Handling က သင့်ရဲ့ Application တွေမှာ အချိန်နဲ့ နေ့ရက်တွေကို အလွယ်တကူ အလုပ်လုပ်စေမှာ ဖြစ်ပါတယ်။ 😊**