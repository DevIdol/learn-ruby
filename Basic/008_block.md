### **Ruby - Blocks**

Ruby မှာ **Blocks** ဟာ Temporary Code Blocks တစ်ခုဖြစ်ပြီး Method တွေနဲ့ တွဲပြီး Run-time မှာ Pass လုပ်တဲ့ Logic တွေကို ဆောင်ရွက်ဖို့ အသုံးပြုပါတယ်။  
**Blocks** တွေကို `{}` သို့မဟုတ် `do...end` နဲ့ သတ်မှတ်တယ်။  

Blocks ဟာ Method သို့ Yield လုပ်တဲ့ Code ကို Pass လုပ်ပြီး Flexibility နဲ့ Reusability ပိုမိုကောင်းမွန်စေတယ်။

---

## **1. Block Syntax**
Ruby Blocks ကို ရေးသားဖို့ **two styles** ရှိတယ်:
1. **Single-line Block** - `{}` သုံးတယ်။
2. **Multi-line Block** - `do...end` သုံးတယ်။

---

### **Single-line Block**
```ruby
[1, 2, 3].each { |num| puts num }
# Output:
# 1
# 2
# 3
```

---

### **Multi-line Block**
```ruby
[1, 2, 3].each do |num|
  puts "Number: #{num}"
end
# Output:
# Number: 1
# Number: 2
# Number: 3
```

---

## **2. Yielding to a Block**
Method တွေဟာ `yield` Keyword ကို သုံးပြီး Block ကို Call လုပ်နိုင်တယ်။

### **Syntax**
```ruby
def method_with_block
  puts "Before the block"
  yield if block_given? # Check if a block is given
  puts "After the block"
end
```

---

### **Example**
```ruby
def greet
  puts "Hello!"
  yield if block_given?
  puts "Goodbye!"
end

greet { puts "This is the block content!" }
# Output:
# Hello!
# This is the block content!
# Goodbye!
```

---

## **3. Passing Parameters to Blocks**
Block သို့ Parameters (Arguments) တွေ Pass လုပ်နိုင်တယ်။

---

### **Example**
```ruby
def greet
  yield("Alice") if block_given?
end

greet { |name| puts "Hello, #{name}!" }
# Output: Hello, Alice!
```

---

## **4. Using `block_given?`**
`block_given?` Method ကို အသုံးပြုပြီး Block ရှိမရှိစစ်ဆေးနိုင်တယ်။

---

### **Example**
```ruby
def optional_block
  if block_given?
    yield
  else
    puts "No block was provided."
  end
end

optional_block        # Output: No block was provided.
optional_block { puts "Block is here!" }  # Output: Block is here!
```

---

## **5. Procs and Lambdas**
Blocks ဟာ Inline Code Blocks ဖြစ်တဲ့အတွက် Object မဟုတ်ဘူး။ Block ကို Object အဖြစ်သုံးချင်ရင် **Proc** သို့မဟုတ် **Lambda** ကို အသုံးပြုနိုင်တယ်။

---

### **Example with Proc**
```ruby
def execute_block(&block)
  block.call if block
end

proc_block = Proc.new { puts "This is a Proc block!" }
execute_block(&proc_block)
# Output: This is a Proc block!
```

---

### **Example with Lambda**
```ruby
my_lambda = ->(name) { puts "Hello, #{name}!" }
my_lambda.call("Alice")
# Output: Hello, Alice!
```

---

## **6. Returning Values from Blocks**
Blocks မှာ Return Value ကို Method ပြန်ပေးစေဖို့ `yield` Return Value ကို ထည့်သုံးနိုင်တယ်။

---

### **Example**
```ruby
def square
  result = yield(4) if block_given?
  puts "Square is #{result}"
end

square { |num| num * num }
# Output: Square is 16
```

---

## **7. Using Blocks with Iterators**
Ruby Iterators (e.g., `each`, `map`, `select`) တွေဟာ Blocks တွေနဲ့ အတူ သုံးနိုင်တယ်။

---

### **Example: `each`**
```ruby
[1, 2, 3].each { |num| puts "Value: #{num}" }
# Output:
# Value: 1
# Value: 2
# Value: 3
```

---

### **Example: `map`**
```ruby
squared = [1, 2, 3].map { |num| num * num }
puts squared.inspect
# Output: [1, 4, 9]
```

---

### **Example: `select`**
```ruby
evens = [1, 2, 3, 4, 5].select { |num| num.even? }
puts evens.inspect
# Output: [2, 4]
```

---

## **8. Nested Blocks**
Ruby Blocks တွေဟာ Nested ဖြစ်နိုင်တယ်၊ လိုအပ်လျှင် Blocks အတွင်းမှာ Blocks သုံးနိုင်တယ်။

---

### **Example**
```ruby
def outer
  yield do
    puts "Inside the inner block"
  end
end

outer do
  puts "Inside the outer block"
  yield
end
# Output:
# Inside the outer block
# Inside the inner block
```

---

## **9. Block Summary**

| **Feature**                     | **Description**                                      | **Example**                                      |
|----------------------------------|----------------------------------------------------|------------------------------------------------|
| **Single-line Block**            | `{}` for simple expressions                        | `numbers.each { |n| puts n }`                  |
| **Multi-line Block**             | `do...end` for complex logic                      | `numbers.each do |n| puts n * 2 end`           |
| **Yield Keyword**                | Calls the passed block                            | `yield(param)`                                 |
| **Check Block with `block_given?`** | Verify if a block was provided                     | `yield if block_given?`                        |
| **Return Values from Blocks**    | Use the result of `yield`                         | `result = yield(value)`                        |
| **Procs and Lambdas**            | Convert Blocks into Callable Objects              | `Proc.new` or `->`                             |
| **Common Methods with Blocks**   | Iterators like `each`, `map`, `select`            | Array and Hash Traversals                      |

---

Ruby Blocks တွေဟာ Flexible Code Design နဲ့ Reusability ရည်ရွယ်ပြီး Object-oriented နဲ့ Functional Programming Concept တွေကို Support လုပ်စေတယ်။ 😊