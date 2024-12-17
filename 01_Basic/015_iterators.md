### **Ruby - Iterators**

Ruby မှာ **Iterator** ဆိုတာ Data Structures (Array, Hash, Range) တွေရဲ့ Elements တွေကို လှည့်ပတ်ဖို့ အသုံးပြုတဲ့ Mechanism ပါ။ Iterators ဟာ Ruby Programming ရဲ့ အခြေခံ Feature တစ်ခုဖြစ်ပြီး Blocks နဲ့ တွဲဖက်သုံးရပါတယ်။

---

## **1. Iterators မိတ်ဆက်**

Iterator တွေကို Ruby မှာ **`each`**, **`times`**, **`upto`**, **`downto`**, **`step`**, **`collect`**, **`map`**, **`select`** တို့လို Method တွေဖြင့် အသုံးပြုနိုင်ပါတယ်။

---

## **2. Common Iterators**

### **2.1 `each` Iterator**
**`each`** ဟာ Array, Hash, Range တို့လို Data Structure တွေရဲ့ Elements တွေကို Iterate လုပ်ရာမှာ အထူးအသုံးများပါတယ်။

#### **For Arrays**
```ruby
numbers = [1, 2, 3, 4, 5]

numbers.each do |number|
  puts number
end
# Output:
# 1
# 2
# 3
# 4
# 5
```

#### **For Hashes**
```ruby
person = { name: "Alice", age: 25 }

person.each do |key, value|
  puts "#{key}: #{value}"
end
# Output:
# name: Alice
# age: 25
```

---

### **2.2 `times` Iterator**
**`times`** Method ကို Specific Number of Times အထိ Loop လုပ်ဖို့ အသုံးပြုနိုင်ပါတယ်။
```ruby
5.times do |i|
  puts "Iteration #{i + 1}"
end
# Output:
# Iteration 1
# Iteration 2
# Iteration 3
# Iteration 4
# Iteration 5
```

---

### **2.3 `upto` Iterator**
**`upto`** Method ကို Number တစ်ခုကနေ တစ်ခုထိ Ascending Order နဲ့ Loop လုပ်ဖို့ အသုံးပြုပါတယ်။
```ruby
1.upto(5) do |i|
  puts i
end
# Output:
# 1
# 2
# 3
# 4
# 5
```

---

### **2.4 `downto` Iterator**
**`downto`** Method ဟာ Descending Order နဲ့ Loop လုပ်ဖို့ အသုံးပြုပါတယ်။
```ruby
5.downto(1) do |i|
  puts i
end
# Output:
# 5
# 4
# 3
# 2
# 1
```

---

### **2.5 `step` Iterator**
**`step`** Method ကို Specific Step Size နဲ့ Loop လုပ်ဖို့ အသုံးပြုပါတယ်။
```ruby
(1..10).step(2) do |i|
  puts i
end
# Output:
# 1
# 3
# 5
# 7
# 9
```

---

## **3. Collecting Results with Iterators**

### **3.1 `collect` or `map`**
**`collect`** (or **`map`**) Method ကို Array ရဲ့ Element တွေကို Transform လုပ်ပြီး New Array အဖြစ် Return ဖို့အသုံးပြုပါတယ်။
```ruby
numbers = [1, 2, 3, 4, 5]
squared_numbers = numbers.map { |num| num * num }

puts squared_numbers.inspect
# Output: [1, 4, 9, 16, 25]
```

---

### **3.2 `select`**
**`select`** Method ကို Array သို့မဟုတ် Hash မှ Filter လုပ်ပြီး Condition ကို ပြည့်မီတဲ့ Values တွေကို Return ဖို့ အသုံးပြုပါတယ်။
```ruby
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = numbers.select { |num| num.even? }
puts even_numbers.inspect
# Output: [2, 4, 6]
```

---

### **3.3 `reject`**
**`reject`** Method ကို `select` ရဲ့ Opposite အနေနဲ့ Condition မပြည့်မီတဲ့ Values တွေကို Return ဖို့ အသုံးပြုပါတယ်။
```ruby
numbers = [1, 2, 3, 4, 5, 6]

odd_numbers = numbers.reject { |num| num.even? }
puts odd_numbers.inspect
# Output: [1, 3, 5]
```

---

## **4. Special Iterators**

### **4.1 Infinite Loops with `loop`**
**`loop`** Method ကို Infinite Loop ဖန်တီးဖို့ အသုံးပြုပါတယ်။
```ruby
count = 0

loop do
  puts "Count: #{count}"
  count += 1
  break if count >= 5
end
# Output:
# Count: 0
# Count: 1
# Count: 2
# Count: 3
# Count: 4
```

---

### **4.2 `each_with_index`**
**`each_with_index`** ဟာ Array သို့မဟုတ် Enumerable Object တစ်ခုရဲ့ Index နဲ့ Element တစ်ပြိုင်နက် Access လုပ်နိုင်ပါတယ်။
```ruby
fruits = ["apple", "banana", "cherry"]

fruits.each_with_index do |fruit, index|
  puts "#{index}: #{fruit}"
end
# Output:
# 0: apple
# 1: banana
# 2: cherry
```

---

### **4.3 `zip`**
**`zip`** Method ကို Multiple Arrays ကို Combine လုပ်ဖို့ အသုံးပြုပါတယ်။
```ruby
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

zipped = names.zip(ages)
puts zipped.inspect
# Output: [["Alice", 25], ["Bob", 30], ["Charlie", 35]]
```

---

## **5. Custom Iterators**

Ruby မှာ **`yield`** နဲ့ Custom Iterator ကို Define လုပ်နိုင်ပါတယ်။
```ruby
def custom_iterator
  puts "Start of iteration"
  yield(1)
  yield(2)
  yield(3)
  puts "End of iteration"
end

custom_iterator do |num|
  puts "Yielded value: #{num}"
end
# Output:
# Start of iteration
# Yielded value: 1
# Yielded value: 2
# Yielded value: 3
# End of iteration
```

---

## **6. Summary Table**

| **Iterator**       | **Usage**                                   | **Example**                     |
|--------------------|---------------------------------------------|---------------------------------|
| `each`             | Iterate over each element                  | `[1, 2].each { |x| puts x }`   |
| `times`            | Loop a specific number of times            | `5.times { puts "Hi" }`        |
| `upto`             | Ascending loop                             | `1.upto(5) { |i| puts i }`     |
| `downto`           | Descending loop                            | `5.downto(1) { |i| puts i }`   |
| `step`             | Loop with step size                        | `(1..10).step(2) { |i| ... }`  |
| `collect`/`map`    | Transform elements                         | `[1, 2].map { |x| x * 2 }`     |
| `select`           | Filter elements                            | `[1, 2, 3].select { |x| x > 1 }` |
| `reject`           | Reject elements                            | `[1, 2, 3].reject { |x| x > 1 }` |
| `each_with_index`  | Iterate with index                         | `["a", "b"].each_with_index`   |
| `zip`              | Combine multiple arrays                    | `[1, 2].zip([3, 4])`           |

---

Ruby Iterators တွေကို Data Structures ပေါ်မှာ လွယ်လွယ်ကူကူ Handle လုပ်နိုင်အောင် Design လုပ်ထားပြီး Code ကို Cleaner နဲ့ Flexible ဖြစ်စေပါတယ်။ 😊