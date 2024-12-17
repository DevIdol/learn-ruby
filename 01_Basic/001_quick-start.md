### **Ruby Syntax**

Ruby သည် Readable, Simple, Flexible ဖြစ်ပြီး Object-Oriented Programming (OOP) မှာ အခြေခံထားတဲ့ Programming Language တစ်ခုဖြစ်ပါတယ်။ Syntax က Human-friendly ဖြစ်လို့ ဖတ်ရှုရလွယ်ကူပြီး Beginner-Friendly ဖြစ်ပါတယ်။

---

## **Basic Ruby Syntax**

### **1. Comments**
Ruby မှာ Comments ကို Code ရဲ့ Notes အနေနဲ့ အသုံးပြုတယ်။
- **Single-line Comment**: `#` နဲ့ရေးတယ်။
- **Multi-line Comment**: `=begin` နဲ့ `=end` အကြားမှာရေးတယ်။

```ruby
# This is a single-line comment

=begin
This is a
multi-line comment.
=end
```

---

### **2. Variables**
Ruby မှာ Variables သည် Value တွေကို Store လုပ်ဖို့သုံးတယ်။ **Dynamic Typing** ဖြစ်လို့ Variable Type ကို Declare မလိုဘဲ Assign လိုက်တာနဲ့သိတယ်။

```ruby
name = "Alice"     # String
age = 25           # Integer
height = 5.7       # Float
is_student = true   # Boolean
```

---

### **3. Data Types**
Ruby မှာ Common Data Types တွေက:
- **String**: `"Hello"`
- **Integer**: `42`
- **Float**: `3.14`
- **Boolean**: `true`, `false`
- **Array**: `[1, 2, 3]`
- **Hash**: `{ key: "value" }`
- **Nil**: `nil` (Null value)

```ruby
string = "Hello"
integer = 42
float = 3.14
boolean = true
array = [1, 2, 3]
hash = { name: "Alice", age: 25 }
nothing = nil
```

---

### **4. Printing to Console**
Ruby မှာ Console Output ပို့ဖို့ `puts`, `print`, `p` ကိုသုံးတယ်။

- **`puts`**: Output နောက်ပိုင်းမှာ newline ထည့်တယ်။
- **`print`**: Output ကို newline မထည့်ဘဲ ရေးတယ်။
- **`p`**: Object အပြည့်အစုံကို Show ပြတယ်။

```ruby
puts "Hello, Ruby!"   # Output: Hello, Ruby!
print "Hello, "       # Output: Hello,
print "World!"        # Output: World!
p [1, 2, 3]           # Output: [1, 2, 3]
```

---

### **5. Control Structures**
#### **If-Else Statements**
```ruby
age = 18
if age >= 18
  puts "You are an adult."
else
  puts "You are a minor."
end
```

#### **Unless Statement**
`unless` ကို Condition မပြည့်မီဆိုရင် Run ဖို့သုံးတယ်။

```ruby
temperature = 30
unless temperature > 35
  puts "It's not too hot."
end
```

#### **Case Statement**
`case` ကို Multiple Conditions Handle ဖို့သုံးတယ်။

```ruby
grade = "B"
case grade
when "A"
  puts "Excellent!"
when "B"
  puts "Good job!"
when "C"
  puts "You passed."
else
  puts "Better luck next time."
end
```

---

### **6. Loops**
#### **While Loop**
```ruby
i = 1
while i <= 5
  puts i
  i += 1
end
```

#### **Until Loop**
`until` ကို Condition မပြည့်မီအထိ Loop လုပ်ဖို့သုံးတယ်။

```ruby
i = 1
until i > 5
  puts i
  i += 1
end
```

#### **For Loop**
```ruby
for i in 1..5
  puts i
end
```

#### **Iterators**
```ruby
(1..5).each do |i|
  puts i
end
```

---

### **7. Methods**
Methods ဟာ Reusable Code တွေကို စုစည်းဖို့ သုံးတယ်။

```ruby
def greet(name)
  puts "Hello, #{name}!"
end

greet("Alice")   # Output: Hello, Alice!
```

---

### **8. Classes and Objects**
Ruby သည် Pure Object-Oriented Language ဖြစ်ပြီး Class တွေက Object တွေဖန်တီးဖို့အသုံးဝင်တယ်။

#### **Example: Class Definition**
```ruby
class Person
  attr_accessor :name, :age

  def initialize(name, age)
    
    @age = age@name = name
  end

  def introduce
    puts "Hi, I'm #{@name} and I'm #{@age} years old."
  end
end

# Create an object
person = Person.new("Alice", 25)
person.introduce   # Output: Hi, I'm Alice and I'm 25 years old.
```

---

### **9. Blocks, Procs, and Lambdas**
#### **Block Example**
```ruby
[1, 2, 3].each do |num|
  puts num * 2
end
```

#### **Proc Example**
```ruby
my_proc = Proc.new { |x| puts x * 2 }
my_proc.call(3)   # Output: 6
```

#### **Lambda Example**
```ruby
my_lambda = ->(x) { puts x * 3 }
my_lambda.call(3)   # Output: 9
```

---

### **10. Exception Handling**
Ruby မှာ Error Handling ကို `begin...rescue...ensure` နဲ့ Handle လုပ်တယ်။

```ruby
begin
  puts 10 / 0
rescue ZeroDivisionError
  puts "You can't divide by zero!"
ensure
  puts "This will always run."
end
```

---

### **11. File I/O**
```ruby
# Write to a file
File.open("example.txt", "w") { |file| file.puts "Hello, Ruby!" }

# Read from a file
File.open("example.txt", "r") { |file| puts file.read }
```

---

### **12. Modules**
Modules ကို Namespace တွေတည်ဆောက်ဖို့နဲ့ Code Reusability အတွက် သုံးတယ်။

#### **Example**
```ruby
module Greetings
  def self.say_hello(name)
    puts "Hello, #{name}!"
  end
end

Greetings.say_hello("Ruby")   # Output: Hello, Ruby!
```

---

## **Ruby Syntax Summary**
| Feature         | Syntax Example                              |
|------------------|--------------------------------------------|
| Variable         | `name = "Alice"`                          |
| Method           | `def method_name; end`                   |
| Conditional      | `if...else`, `case`                      |
| Loop             | `while`, `for`, `each`                   |
| Class            | `class ClassName; end`                   |
| Module           | `module ModuleName; end`                 |
| File I/O         | `File.open("file.txt", "r")`             |
| Exception        | `begin...rescue...ensure`                |

Ruby Syntax သည် ရိုးရှင်းပြီး Flexible ဖြစ်လို့ Code ရေးသားရတာ မျှတသက်သာစေပါတယ်! 😊