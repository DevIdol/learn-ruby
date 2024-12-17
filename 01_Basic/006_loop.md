### **Ruby - Loops**

Ruby မှာ Loops တွေကို Code ကို Repeatedly Execute လုပ်ဖို့ အသုံးပြုတယ်။ Iterative Logic တွေကို ချုပ်ချာပြီး ရေးသားနိုင်စေတယ်။  
Ruby Loops တွေမှာ Iterators တွေ၊ Control Statements (e.g., `break`, `next`)၊ နဲ့ Reusable Code Blocks တွေပါဝင်တယ်။

---

## **1. while Loop**
`while` Loop ကို **condition true ဖြစ်နေချိန်တိုင်အောင်** Loop ပြောင်းသုံးတယ်။

### **Syntax**
```ruby
while condition
  # Code to execute
end
```

---

### **Example**
```ruby
x = 1

while x <= 5
  puts "Value: #{x}"
  x += 1
end
# Output:
# Value: 1
# Value: 2
# Value: 3
# Value: 4
# Value: 5
```

---

## **2. until Loop**
`until` Loop ဟာ **condition false ဖြစ်နေချိန်တိုင်အောင်** Loop ပြောင်းသုံးတယ်။

### **Syntax**
```ruby
until condition
  # Code to execute
end
```

---

### **Example**
```ruby
x = 1

until x > 5
  puts "Value: #{x}"
  x += 1
end
# Output:
# Value: 1
# Value: 2
# Value: 3
# Value: 4
# Value: 5
```

---

## **3. for Loop**
`for` Loop ကို Iteration-based Task တွေ အတွက် သုံးတယ်။ **Ranges** သို့မဟုတ် **Arrays** တွေပေါ်မှာ iterate လုပ်တယ်။

### **Syntax**
```ruby
for variable in range_or_array
  # Code to execute
end
```

---

### **Example**
```ruby
for i in 1..5
  puts "Value: #{i}"
end
# Output:
# Value: 1
# Value: 2
# Value: 3
# Value: 4
# Value: 5
```

---

### **Iterating Over Arrays**
```ruby
fruits = ["apple", "banana", "cherry"]

for fruit in fruits
  puts "I like #{fruit}"
end
# Output:
# I like apple
# I like banana
# I like cherry
```

---

## **4. times Loop**
`times` Loop ကို **Numeric Iteration** အတွက်သုံးတယ်။ Zero-based Counting ဖြစ်တယ်။

### **Syntax**
```ruby
number.times do
  # Code to execute
end
```

---

### **Example**
```ruby
5.times do |i|
  puts "Iteration: #{i}"
end
# Output:
# Iteration: 0
# Iteration: 1
# Iteration: 2
# Iteration: 3
# Iteration: 4
```

---

## **5. each Iterator**
`each` Iterator ကို Arrays, Hashes, Ranges အပေါ်မှာ Iteration လုပ်ဖို့ သုံးတယ်။

### **Syntax**
```ruby
collection.each do |item|
  # Code to execute
end
```

---

### **Example (Array)**
```ruby
names = ["Alice", "Bob", "Charlie"]

names.each do |name|
  puts "Hello, #{name}!"
end
# Output:
# Hello, Alice!
# Hello, Bob!
# Hello, Charlie!
```

### **Example (Hash)**
```ruby
person = {name: "Alice", age: 25}

person.each do |key, value|
  puts "#{key}: #{value}"
end
# Output:
# name: Alice
# age: 25
```

---

## **6. loop Do**
`loop do` ကို Infinite Loop လုပ်ဖို့ သုံးတယ်။ Control Statements (`break`, `next`) မပါရင် Forever Loop ဖြစ်တယ်။

### **Syntax**
```ruby
loop do
  # Code to execute
  break if condition
end
```

---

### **Example**
```ruby
x = 1

loop do
  puts "Value: #{x}"
  x += 1
  break if x > 5
end
# Output:
# Value: 1
# Value: 2
# Value: 3
# Value: 4
# Value: 5
```

---

## **7. Control Statements**
### **1. break**
Loop ကို Stop လုပ်တယ်။
```ruby
x = 1

while x <= 10
  puts x
  break if x == 5
  x += 1
end
# Output: 1 2 3 4 5
```

### **2. next**
Current Iteration ကို Skip လုပ်ပြီး နောက် Iteration သို့ ဆက်လုပ်တယ်။
```ruby
(1..5).each do |i|
  next if i == 3
  puts i
end
# Output: 1 2 4 5
```

### **3. redo**
Current Iteration ကို ပြန်လုပ်တယ်။
```ruby
i = 0
while i < 5
  i += 1
  redo if i == 3
  puts i
end
# Output: Infinite Loop (3 is repeated)
```

---

## **8. until Modifier**
**Single-line until** အတွက် `do` သုံးစွဲမရပါ။
```ruby
x = 1
puts x += 1 until x > 5
# Output: 6
```

---

## **9. Loop with Range and Step**
```ruby
(1..10).step(2) do |i|
  puts "Step: #{i}"
end
# Output:
# Step: 1
# Step: 3
# Step: 5
# Step: 7
# Step: 9
```

---

## **Summary Table**

| **Loop Type** | **Best Use Case**                    | **Control Mechanism**               |
|---------------|-------------------------------------|-------------------------------------|
| `while`       | Condition-based Repetition          | Loop until condition is `false`    |
| `until`       | Repeats until condition is `true`   | Loop until condition is `true`     |
| `for`         | Range or Collection Iteration       | Predefined Range/Array             |
| `times`       | Numeric Iteration                  | Zero-based Count                   |
| `each`        | Iterate over Array/Hash/Range      | Dynamic Collections                |
| `loop`        | Infinite Loop (with break/next)    | Manual Control                     |

Ruby Loops တွေကို Flexible Logic တည်ဆောက်ဖို့ အသုံးပြုနိုင်ပြီး Control Statements တွေဖြင့် Loops ကို ပိုထိထိရောက်ရောက် Manage လုပ်နိုင်တယ်။ 😊