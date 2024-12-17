### **Ruby - Exceptions**

Ruby မှာ **Exceptions** ဟာ Error Handling အတွက် အသုံးပြုတဲ့ Mechanism တစ်ခုပါ။ Code တစ်ခုမှာ အမှား (Error) တစ်ခုဖြစ်လာတဲ့အခါ၊ Exception ကို **`raise`** ကနေ လုပ်ဆောင်နိုင်ပြီး၊ **`begin...rescue...end`** ပုံစံဖြင့် Exception Handling ကို ပြုလုပ်နိုင်ပါတယ်။

---

## **1. What is an Exception?**
Exception ဆိုတာ ရိုးရိုး **Error** မဟုတ်ပါဘူး။ Error ဖြစ်ပြီးတဲ့အခါမှာ program ရဲ့ Execution ကို တစ်ခါတစ်လေ ချန်ထားဖို့လိုတာမျိုး ဖြစ်တတ်ပါတယ်။ Ruby မှာ Exception Handling ကို ပိုပြီး မြှင့်တင်ပြီး, **`rescue`**, **`ensure`**, **`raise`** တို့လို စကားလုံးများကို အသုံးပြုပါတယ်။

---

## **2. Basic Syntax: `begin...rescue...end`**

Ruby မှာ **`begin...rescue...end`** ပုံစံဟာ Exception Handling ကို လုပ်နိုင်ဖို့ သုံးရတဲ့ Basic Structure ဖြစ်ပါတယ်။

```ruby
begin
  # Code that might raise an exception
  num = 10 / 0  # This will raise a ZeroDivisionError
rescue ZeroDivisionError => e
  # Code that will run if an exception occurs
  puts "Error occurred: #{e.message}"
ensure
  # This block always runs whether exception occurs or not
  puts "This will always be executed."
end
```

### **Explanation**
- **`begin`**: Exception-raising code block ကို စတင်လိုက်တဲ့နေရာ
- **`rescue`**: Exception ဖြစ်ရတဲ့အခါ ဖြေရှင်းဖို့ code block
- **`ensure`**: Exception ဖြစ်ပေမယ့် မဖြစ်ပဲ လုပ်ဆောင်ချင်တဲ့ block (Optional)

---

## **3. Types of Exceptions in Ruby**

Ruby မှာ Exception များစွာရှိပြီး အကြောင်းပြချက်အမျိုးမျိုးကြောင့် Exception ကို Raise လုပ်နိုင်ပါတယ်။

### **3.1 StandardError**
**StandardError** သည် Ruby မှာ default exception class ဖြစ်ပြီး၊ ဒါဟာ mostly အမှားတွေကို handle လုပ်ပါတယ်။
```ruby
begin
  raise StandardError, "This is a standard error"
rescue StandardError => e
  puts "Caught an exception: #{e.message}"
end
```

### **3.2 Built-in Exceptions**
Ruby တွင် built-in Exception Types များကတော့:

- **`ZeroDivisionError`**: Number ကို 0 နဲ့မစားရင် generation။
- **`ArgumentError`**: Function/Method မတော်တဆပေါင်းခြင်း။
- **`TypeError`**: Type မတူတဲ့ value ကို operation လုပ်ခြင်း။
- **`NameError`**: Variable, method, or class ကို မတွေ့ရင် generation။
- **`NoMethodError`**: Object ပေါ်မှာ အတည်ပြုထားတဲ့ method မရှိပါ။
- **`IOError`**: File reading/writing related issues။
- **`RuntimeError`**: Unspecified runtime issues.

---

## **4. Raising Exceptions with `raise`**

Exception ကို **`raise`** သုံးပြီး မိမိအတွက်လိုအပ်တဲ့ Exception ကို manually ဖြည့်စွက်နိုင်ပါတယ်။

```ruby
def check_age(age)
  raise ArgumentError, "Age must be a positive number!" if age <= 0
  puts "Age is #{age}"
end

begin
  check_age(-5)
rescue ArgumentError => e
  puts "Caught exception: #{e.message}"
end
```

**Output:**
```
Caught exception: Age must be a positive number!
```

### **Explanation:**
- **`raise`** ကို Exception ကို Throw လုပ်ရန် သုံးသည်။
- Exception မှာ message လည်းပေးနိုင်သည်။

---

## **5. Handling Multiple Exceptions**

Ruby မှာ **`rescue`** ကို Multiple Exceptions နဲ့ Handle လုပ်နိုင်ပါတယ်။

```ruby
begin
  # some code that might raise an exception
  num = 10 / 0
rescue ZeroDivisionError => e
  puts "Caught ZeroDivisionError: #{e.message}"
rescue StandardError => e
  puts "Caught a general exception: #{e.message}"
end
```

### **Explanation:**
- **`rescue`** ခေါ်တဲ့အခါမှာ Exception အမျိုးအစားကိုပဲ ရွေးချယ်ပြီး Handle လုပ်နိုင်ပါသည်။

---

## **6. Custom Exceptions**

Ruby တွင် Custom Exception Class များကို ပြုလုပ်ပြီး error handling ကို ပိုမိုထိရောက်စေဖို့အသုံးပြုနိုင်ပါတယ်။

### **6.1 Define Custom Exception**
```ruby
class CustomError < StandardError
end

def raise_custom_error
  raise CustomError, "This is a custom error"
end

begin
  raise_custom_error
rescue CustomError => e
  puts "Caught custom error: #{e.message}"
end
```

---

## **7. Retry Logic in Exception Handling**

Sometimes you might want to **retry** an operation after an exception occurs.

```ruby
count = 0
begin
  count += 1
  puts "Attempt #{count}"
  raise "Something went wrong" if count < 3
rescue => e
  puts "Error occurred: #{e.message}. Retrying..."
  retry if count < 3
end
```

### **Explanation:**
- **`retry`** သည် Exception ဖြစ်ပြီးပြီးနောက် အလုပ်လုပ်ရပ်လို့နောက်တခါစတင်နိုင်ခြင်း။

---

## **8. Ensure Block**

**`ensure`** ဟာ Exception မဖြစ်ပဲ အဆင်ပြေကာလည်း run ပါလိမ့်မယ်။

```ruby
begin
  # some code
  puts "Trying to open a file"
  raise IOError, "File not found"  # Example of an error
rescue IOError => e
  puts "Caught exception: #{e.message}"
ensure
  puts "This will always run, regardless of an exception."
end
```

**Output:**
```
Trying to open a file
Caught exception: File not found
This will always run, regardless of an exception.
```

---

## **9. Example: Handling Multiple Exceptions**

```ruby
def divide_numbers(a, b)
  begin
    result = a / b
    puts "Result: #{result}"
  rescue ZeroDivisionError => e
    puts "Error: Division by zero is not allowed!"
  rescue TypeError => e
    puts "Error: Invalid data type!"
  rescue => e
    puts "Some other error occurred: #{e.message}"
  end
end

divide_numbers(10, 2)      # Result: 5
divide_numbers(10, 0)      # Error: Division by zero is not allowed!
divide_numbers(10, 'a')    # Error: Invalid data type!
```

---

Ruby မှာ **Exception Handling** သည် Code Error များကို ကြိုတင်သိရှိပြီး **`begin...rescue...end`** block နဲ့ handle လုပ်နိုင်ရန်အတွက် အလွန်အသုံးဝင်သော Mechanism တစ်ခုဖြစ်ပါတယ်။ **`raise`** ကိုအသုံးပြုပြီး Custom Exceptions များကိုလည်း ဖန်တီးနိုင်ပြီး error ဖြစ်တဲ့အချိန်မှာ **`rescue`** နဲ့ exception ကို handle လုပ်ပြီး program ကို **`ensure`** block ဖြင့် process ချင်းကို finalize လုပ်နိုင်ပါတယ်။