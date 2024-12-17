### **Ruby - Regular Expressions (Regex)**

Ruby မှာ **Regular Expressions (Regex)** ကို string manipulation တွေ၊ pattern matching တွေနဲ့ လုပ်ဆောင်တဲ့အခါ အလွန်အရေးကြီးတဲ့ tools တွေဖြစ်ပါတယ်။ Regex က string များထဲမှ pattern တွေကို ရှာဖွေခြင်း၊ ပြောင်းလဲခြင်း၊ validate လုပ်ခြင်း စတာတွေကို လုပ်နိုင်ပါတယ်။ Ruby မှာ Regex ကို **`/pattern/`** ဆိုပြီး သတ်မှတ်ကြသည်။

---

## **1. What is Regular Expression?**
Regular Expressions (Regex) သည် pattern matching tool တစ်ခုဖြစ်ပြီး, text (string) တွေကို pattern များနှင့် တိုက်စက်ကြည့်ပြီး filter လုပ်တဲ့ mechanism ပါ။ Regex သည် **search**, **replace**, **validate**, **split**, **match** လုပ်ရန် အရမ်းအသုံးဝင်ပါတယ်။

---

## **2. Basic Syntax of Regular Expressions**

Ruby မှာ Regex ကို **`/pattern/`** ပုံစံနဲ့ သတ်မှတ်ပါတယ်။ Regular Expressions ရဲ့ Syntax တွေကို စိတ်ကြိုက်သတ်မှတ်နိုင်ပါတယ်။

### **2.1 Matching Strings**

Regex pattern ကို **`=~`** operator နှင့် တစ်နေရာမှာ compare လုပ်နိုင်ပါတယ်။

```ruby
str = "Hello, Ruby!"
if str =~ /Ruby/
  puts "Pattern found!"
else
  puts "Pattern not found!"
end
```

**Explanation:**
- **`=~`** operator က string ထဲမှာ regex pattern ကို ရှာပြီး matching ဖြစ်ရင် **`true`** ကို return ပြန်ပါသည်။
- "Ruby" ဆိုတာ regex pattern ဖြစ်ပြီး၊ string "Hello, Ruby!" ထဲမှာ ရှိလို့ "Pattern found!" လို့ output ဖြစ်ပါတယ်။

---

## **3. Common Regular Expressions Metacharacters**

Regex တွင် မတူညီသော symbols တွေ၊ metacharacters တွေကို အသုံးပြုပြီး pattern တွေကို ပိုမိုအတိအကျ ရှာဖွေနိုင်ပါတယ်။

### **3.1 `.` (Dot)**

Dot (`.`) ဆိုတာ အားလုံးသော character များကို အစားထိုးဖော်ပြနိုင်တဲ့ character ပါ။

```ruby
str = "Hello"
if str =~ /H.llo/
  puts "Pattern found!"
else
  puts "Pattern not found!"
end
```

**Explanation:**
- **`/H.llo/`** ဟာ "Hello", "Hullo", "Hxllo" စသဖြင့် any character (except newline) ရှိတဲ့ string များကို match လုပ်နိုင်ပါတယ်။

### **3.2 `^` (Caret) and `$` (Dollar)**

- **`^`**: Pattern ကို string ၏အစမှာရှိရန် ရည်ရွယ်သည်။
- **`$`**: Pattern ကို string ၏အဆုံးမှာရှိရန် ရည်ရွယ်သည်။

```ruby
str = "Hello, world"
if str =~ /^Hello/
  puts "Starts with 'Hello'"
end

if str =~ /world$/
  puts "Ends with 'world'"
end
```

**Explanation:**
- **`/^Hello/`**: "Hello" က string ၏အစမှာရှိတဲ့နေရာတွေကို match လုပ်ပါတယ်။
- **`/world$/`**: "world" က string ၏အဆုံးမှာရှိတဲ့နေရာတွေကို match လုပ်ပါတယ်။

### **3.3 `[]` (Square Brackets)**

Square brackets (`[]`) ကို character set တွေကို သတ်မှတ်ရန် အသုံးပြုနိုင်ပါသည်။ Square brackets မှာ character များကို ရှေ့သို့ပေါင်းစပ်ထားနိုင်ပါသည်။

```ruby
str = "apple"
if str =~ /[aeiou]/
  puts "Vowel found!"
end
```

**Explanation:**
- **`/[aeiou]/`** ဟာ "apple" တွင် **a**, **e**, **i**, **o**, **u** မှာ ရှိတဲ့ vowels တစ်ခုခုကို ရှာပါတယ်။

### **3.4 `*`, `+`, and `?`**

- **`*`**: The preceding element (character) may repeat 0 or more times.
- **`+`**: The preceding element (character) may repeat 1 or more times.
- **`?`**: The preceding element (character) may repeat 0 or 1 time.

```ruby
# * (zero or more)
str = "looooong"
if str =~ /lo*ng/
  puts "Pattern found!"
end

# + (one or more)
str = "loong"
if str =~ /lo+ng/
  puts "Pattern found!"
end

# ? (zero or one)
str = "abc"
if str =~ /ab?c/
  puts "Pattern found!"
end
```

**Explanation:**
- **`lo*ng`**: `*` ကို အသုံးပြု၍ "lo" ကို 0 ဒါမှမဟုတ် အများအပြား "o" characters နှင့် အပြီး "ng" ဖြစ်သည့် pattern ကို match လုပ်နိုင်ပါတယ်။
- **`lo+ng`**: `+` ကို အသုံးပြု၍ "lo" ကို 1 ဒါမှမဟုတ် အများအပြား "o" characters နှင့် အပြီး "ng" ဖြစ်သည့် pattern ကို match လုပ်နိုင်ပါတယ်။
- **`ab?c`**: `?` ကို အသုံးပြု၍ "ab" ဟာ 0 ဒါမှမဟုတ် 1 "b" character များနှင့် အပြီး "c" ဖြစ်သော string တွေကို match လုပ်နိုင်ပါတယ်။

### **3.5 `|` (Alternation)**

Alternation (`|`) ကို "or" operator အဖြစ် အသုံးပြုနိုင်ပါတယ်။

```ruby
str = "hello"
if str =~ /hello|hi/
  puts "Pattern found!"
end
```

**Explanation:**
- **`/hello|hi/`** မှာ **`|`** သည် "hello" သို့မဟုတ် "hi" တို့ထဲမှ တစ်ခုခုဖြစ်ပါက match လုပ်ပါသည်။

---

## **4. Grouping and Capturing with Parentheses**

### **4.1 Parentheses for Grouping**

Parentheses (`()`) ကို pattern ကို group လုပ်ဖို့ အသုံးပြုနိုင်ပါတယ်။

```ruby
str = "Hello 123"
if str =~ /(Hello) (\d+)/
  puts "Match found!"
end
```

**Explanation:**
- **`/(Hello) (\d+)/`** သည် "Hello" နှင့် digit များ (number) ကို အပိုင်းသီးသန့် group များအဖြစ် အသုံးပြုနေပါသည်။

### **4.2 Capturing Groups**

Captured groups ကို **`\1`, `\2`, ...** နဲ့ အသုံးပြုနိုင်ပါတယ်။

```ruby
str = "Hello 123"
if str =~ /(Hello) (\d+)/
  puts "Captured: #{$1} and #{$2}"
end
```

**Explanation:**
- **`$1`, `$2`** က captured groups ဖြစ်ပြီး၊ "Hello" နှင့် "123" ကို 각각 capture လုပ်ထားပါတယ်။

---

## **5. Regex Methods in Ruby**

Ruby မှာ Regex နဲ့ပတ်သက်တဲ့ method များကို လည်း အသုံးပြုနိုင်ပါတယ်။ ရိုးရိုး string method တွေနဲ့ regex လုပ်ဆောင်နိုင်သလို, **`match`**, **`scan`**, **`sub`**, **`gsub`** စသည့် method တွေနဲ့ ပိုပြီး advanced manipulations ပြုလုပ်နိုင်ပါတယ်။

### **5.1 `=~` Operator**

```ruby
str = "Hello"
if str =~ /Hello/
  puts "Pattern matched!"
end
```

### **5.2 `match` Method**

```ruby
str = "Hello Ruby"
match_data = str.match(/Ruby/)
puts match_data[0]  # Outputs: Ruby
```

### **5.3 `scan` Method**

```ruby
str = "one two three"
matches = str.scan(/\w+/)
puts matches.inspect  # Outputs: ["one", "two", "three"]
```

### **5.4 `sub` and `gsub` Methods**

- **`sub`**: First match only.
- **`gsub`**: All matches.

```ruby
str = "Hello world"
puts str.sub(/world/, "Ruby")  # Outputs: Hello Ruby

str = "Hello world world"
puts str.gsub(/world/, "Ruby")  # Outputs: Hello Ruby Ruby
```

---

## **6. Example: Validate an Email Address**

```ruby
email = "user@example.com"
if email =~ /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i
  puts "Valid email address"
else
  puts "Invalid email address"
end
```

**Explanation:**
- The regex pattern here is used to validate an email format. **`\A`** and **`\z`** match the start and end of the string respectively.

---

Ruby မှာ **Regular Expressions** (Regex) ကို string matching, search, replace, validation, split, and manipulation စတဲ့ လုပ်ဆောင်ချက်တွေကို အလွယ်တကူ ပြုလုပ်နိုင်ပါတယ်။ Regex တွေက string တွေမှာ pattern matching လုပ်တဲ့အခါ အသုံးဝင်ပြီး, Ruby က Regex အတွက် built-in support ပေးတဲ့ syntax တွေကို အသုံးပြုနိုင်ပါတယ်။ Regex ကို master လုပ်လျှင်, string manipulation တွေကို အလွယ်တကူ and efficiently လုပ်နိုင်မှာ ဖြစ်ပါတယ်။