### **Ruby - if...else, case, unless**

Ruby မှာ Conditional Statements တွေကို Program Logic တွေကို ထိန်းချုပ်ဖို့ အသုံးပြုတယ်။  
`if...else`, `case`, နဲ့ `unless` ဟာ Ruby Programming Language မှာ အသုံးများတဲ့ Conditional Constructs တွေဖြစ်ပါတယ်။

---

## **1. if...else Statement**
`if...else` ဟာ Ruby ရဲ့ အခြေခံ Conditional Statement ဖြစ်ပြီး, **condition true ဖြစ်မယ်ဆိုရင် code block ကို run လုပ်ပြီး** false ဖြစ်ရင် အခြား code block ကို run လုပ်တယ်။

### **Syntax**
```ruby
if condition
  # Code to execute if condition is true
elsif another_condition
  # Code to execute if another_condition is true
else
  # Code to execute if no condition is true
end
```

---

### **Example**
```ruby
x = 10

if x > 15
  puts "x is greater than 15"
elsif x == 10
  puts "x is exactly 10"
else
  puts "x is less than 10"
end
# Output: x is exactly 10
```

---

### **One-liner if**
Ruby တွင် Short Conditions အတွက် Single-line Syntax သုံးနိုင်သည်။
```ruby
puts "x is greater than 10" if x > 10
```

---

## **2. case Statement**
`case` Statement ကို Multiple Conditions တွေကို Handle လုပ်ဖို့ သုံးတယ်။ **Switch-case statement** သဘောမျိုးဖြစ်ပြီး, **Readable** နဲ့ **Shorter** ဖြစ်တယ်။

### **Syntax**
```ruby
case expression
when value1
  # Code to execute if expression == value1
when value2
  # Code to execute if expression == value2
else
  # Code to execute if no condition matches
end
```

---

### **Example**
```ruby
day = "Monday"

case day
when "Monday"
  puts "Start of the work week!"
when "Friday"
  puts "Almost the weekend!"
when "Saturday", "Sunday"
  puts "Weekend vibes!"
else
  puts "Midweek grind!"
end
# Output: Start of the work week!
```

---

### **Case with Range**
Case statement can work with ranges.
```ruby
age = 25

case age
when 0..12
  puts "Child"
when 13..19
  puts "Teenager"
when 20..59
  puts "Adult"
else
  puts "Senior"
end
# Output: Adult
```

---

## **3. unless Statement**
`unless` ကို `if not` အစား သုံးတယ်။  
Condition **false ဖြစ်မှ code block ကို run လုပ်တယ်**။

### **Syntax**
```ruby
unless condition
  # Code to execute if condition is false
else
  # Code to execute if condition is true
end
```

---

### **Example**
```ruby
age = 15

unless age >= 18
  puts "You are not allowed to vote."
else
  puts "You can vote."
end
# Output: You are not allowed to vote.
```

---

### **One-liner unless**
```ruby
puts "You cannot drive." unless age >= 16
```

---

## **Comparison of `if` vs `unless`**
- Use `if` for **true-based conditions**.
- Use `unless` for **false-based conditions**.

### **Example**
```ruby
x = 10

puts "x is greater than 5" if x > 5
puts "x is not greater than 5" unless x > 5
```

---

## **4. Nested Conditions**
Ruby ထဲမှာ Conditions တွေကို Nest လုပ်ပြီး Logical Decision-making ကို အခြေခံ လုပ်နိုင်တယ်။

### **Example**
```ruby
x = 20

if x > 10
  if x % 2 == 0
    puts "x is greater than 10 and even."
  else
    puts "x is greater than 10 and odd."
  end
else
  puts "x is 10 or less."
end
# Output: x is greater than 10 and even.
```

---

## **5. Ternary Operator**
Ternary Operator ဟာ `if...else` ရဲ့ Short Syntax ဖြစ်ပြီး, **Single-line condition** handling အတွက် သုံးတယ်။

### **Syntax**
```ruby
condition ? true_case : false_case
```

---

### **Example**
```ruby
x = 5
puts x > 3 ? "Greater" : "Smaller"
# Output: Greater
```

---

## **6. Logical Operators with Conditions**
`&&`, `||`, `!` Operators တွေကို Conditional Statements တွေနဲ့ တွဲသုံးနိုင်တယ်။

### **Example**
```ruby
age = 20

if age >= 18 && age <= 25
  puts "You are a young adult."
elsif age > 25
  puts "You are an adult."
else
  puts "You are a minor."
end
# Output: You are a young adult.
```

---

## **Summary Table**

| **Construct**   | **Use Case**                              | **Syntax** Example                                         |
|------------------|-------------------------------------------|-----------------------------------------------------------|
| `if...else`      | For True/False conditions                | `if x > 5; puts "Hi"; else; puts "Bye"; end`             |
| `case`           | For Multiple Conditions                  | `case day; when "Mon"; puts "Work"; else; puts "Rest"; end` |
| `unless`         | For False conditions                     | `unless x > 5; puts "Small"; end`                        |
| Ternary Operator | Compact `if...else`                      | `x > 5 ? "Big" : "Small"`                                |

Ruby Conditional Constructs တွေကို Flexible Syntax နဲ့ ရိုးရှင်းစွာ အသုံးပြုနိုင်တယ်။ 😊