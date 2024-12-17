### **Ruby - Methods**

Ruby မှာ **Methods** ဟာ Code Reusability နဲ့ Logic Separation အတွက် အသုံးများတဲ့ အခန်းကဏ္ဍတစ်ခု ဖြစ်တယ်။  
**Method** ဆိုတာ နာမည်ပေးထားတဲ့ Code Block တစ်ခုဖြစ်ပြီး၊ လိုအပ်တဲ့အချိန်မှာ Call လုပ်ပြီး အသုံးပြုနိုင်တယ်။

---

## **1. Method Definition**
### **Syntax**
```ruby
def method_name(parameters)
  # Code to execute
end
```

- **`def`**: Method definition ကို စတင်တည်ဆောက်ဖို့သုံးသည်။
- **`method_name`**: Method ရဲ့ နာမည်၊ lowercase နဲ့ snake_case ဖြစ်ရမည်။
- **`parameters`**: Input Arguments (Optional) ဖြစ်သည်။
- **`end`**: Method Definition ကို သတ်မှတ်ဖို့ အဆုံးမှာသုံးသည်။

---

### **Example**
```ruby
def greet(name)
  puts "Hello, #{name}!"
end

greet("Alice")  # Output: Hello, Alice!
```

---

## **2. Method Parameters**
Ruby Method တွေမှာ Parameters (Inputs) တွေကို Pass လုပ်နိုင်တယ်။  
Default Parameters, Variable Parameters, နဲ့ Keyword Arguments တွေကိုလည်း Ruby မှာ Support လုပ်တယ်။

---

### **Example with Parameters**
```ruby
def add(a, b)
  a + b
end

puts add(5, 3)  # Output: 8
```

---

### **Default Parameters**
Default Value ကို Parameters အတွက် သတ်မှတ်နိုင်တယ်။
```ruby
def greet(name = "World")
  puts "Hello, #{name}!"
end

greet          # Output: Hello, World!
greet("Alice") # Output: Hello, Alice!
```

---

### **Variable-Length Arguments (`*args`)**
**`*args`** ကို အသုံးပြုပြီး Multiple Parameters ကို Array အဖြစ် Handle လုပ်နိုင်တယ်။
```ruby
def sum(*numbers)
  numbers.sum
end

puts sum(1, 2, 3, 4)  # Output: 10
puts sum(10, 20)      # Output: 30
```

---

### **Keyword Arguments**
Ruby မှာ Named Parameters (Key-value pairs) ကို Keyword Arguments အဖြစ် သုံးနိုင်တယ်။
```ruby
def user_info(name:, age:)
  puts "Name: #{name}, Age: #{age}"
end

user_info(name: "Alice", age: 25)  # Output: Name: Alice, Age: 25
```

---

## **3. Method Return Values**
Ruby Method တွေဟာ Default အနေနဲ့ နောက်ဆုံး Expression ကို Return လုပ်တယ်။

---

### **Example**
```ruby
def multiply(a, b)
  a * b  # Last expression is automatically returned
end

puts multiply(5, 3)  # Output: 15
```

---

### **Using `return` Keyword**
`return` Keyword ကို Explicitly Return လုပ်ဖို့ သုံးနိုင်တယ်။
```ruby
def divide(a, b)
  return "Cannot divide by zero!" if b == 0
  a / b
end

puts divide(10, 2)  # Output: 5
puts divide(10, 0)  # Output: Cannot divide by zero!
```

---

## **4. Method Calling**
Method ကို Call လုပ်ဖို့ **Method Name** ကို ရေးပြီး Argument တွေကို Pass လုပ်တယ်။  
Arguments မရှိတဲ့ Method ကို Parentheses လည်း မလိုပါဘဲ Call လုပ်နိုင်တယ်။

---

### **Example**
```ruby
def greet
  puts "Hello!"
end

greet          # Output: Hello!
greet()        # Output: Hello!
```

---

## **5. Method with Block**
Ruby Methods တွေဟာ Blocks တွေနဲ့ တွဲပြီး သုံးနိုင်တယ်။ Block တွေဟာ Temporary Code Blocks ဖြစ်ပြီး `{}` သို့မဟုတ် `do...end` ဖြင့် သတ်မှတ်တယ်။

---

### **Example**
```ruby
def repeat(times)
  times.times { yield }  # Call the block
end

repeat(3) { puts "Ruby!" }
# Output:
# Ruby!
# Ruby!
# Ruby!
```

---

### **Using Block with Parameters**
```ruby
def repeat_message(times)
  times.times { |i| yield(i) }
end

repeat_message(3) { |i| puts "Iteration: #{i}" }
# Output:
# Iteration: 0
# Iteration: 1
# Iteration: 2
```

---

## **6. Method Aliases**
`alias` Keyword ကို သုံးပြီး Method Name ကို Alternate Name နဲ့ သုံးနိုင်တယ်။

---

### **Example**
```ruby
def greet
  puts "Hello!"
end

alias say_hello greet
say_hello  # Output: Hello!
```

---

## **7. Private and Protected Methods**
Ruby Classes အတွင်း Methods တွေကို Visibility Control ပြုလုပ်နိုင်တယ်။

### **Private Methods**
Private Methods ကို Class အတွင်းမှသာ Access လုပ်နိုင်တယ်။
```ruby
class Example
  def public_method
    puts "This is public."
    private_method
  end

  private

  def private_method
    puts "This is private."
  end
end

obj = Example.new
obj.public_method  # Output: This is public. This is private.
# obj.private_method  # Error: private method `private_method'
```

---

### **Protected Methods**
Protected Methods ကို Same Class (သို့) Subclass ထဲက Object တွေကြားမှသာ Call လုပ်နိုင်တယ်။
```ruby
class Example
  protected

  def protected_method
    puts "This is protected."
  end

  public

  def call_protected(other)
    other.protected_method
  end
end

obj1 = Example.new
obj2 = Example.new
obj1.call_protected(obj2)  # Output: This is protected.
```

---

## **8. Summary Table**

| **Feature**              | **Syntax/Use Case**                                    |
|--------------------------|-------------------------------------------------------|
| **Method Definition**     | `def method_name; end`                               |
| **Default Parameters**    | `def greet(name = "World"); end`                     |
| **Variable Arguments**    | `def sum(*args); end`                                |
| **Keyword Arguments**     | `def user_info(name:, age:); end`                    |
| **Block with `yield`**    | `def repeat; yield; end`                             |
| **Return Values**         | Automatically return the last expression             |
| **Private/Protected**     | Control method access within or across objects       |

Ruby Methods တွေကို Flexible Logic, Reusability, နဲ့ Advanced Constructs တွေနဲ့ အချိန်တိုအတွင်း စီမံခန့်ခွဲနိုင်ပါတယ်။ 😊