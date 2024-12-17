### **Ruby - Variables, Constants, and Literals**

Ruby သည် Dynamic Typing Programming Language ဖြစ်တာကြောင့် Variables, Constants, Literals တွေကို အသုံးပြုရတာ လွယ်ကူပြီး Flexible ဖြစ်ပါတယ်။

---

## **1. Variables**
Ruby မှာ **Variables** ဆိုတာ Data ကို Temporary Store လုပ်တဲ့ Containers လို့ဆိုနိုင်ပါတယ်။  
**Dynamic Typing** လုပ်ပုံကြောင့် Variable Type ကို Predefine မလုပ်ရပါဘူး။

### **Variable Naming Rules**
- Variable names must start with a **lowercase letter** or an **underscore (`_`)**.
- Cannot start with a number or contain special characters.
- Ruby is **case-sensitive**, so `myVar` and `myvar` are different.

---

### **Variable Types in Ruby**

| **Type**              | **Description**                                                              | **Example**               |
|------------------------|------------------------------------------------------------------------------|---------------------------|
| **Local Variable**     | Accessible only within a specific method or block.                          | `name = "Alice"`          |
| **Instance Variable**  | Belongs to a specific object, starts with `@`.                              | `@age = 25`               |
| **Class Variable**     | Shared among all instances of a class, starts with `@@`.                    | `@@count = 0`             |
| **Global Variable**    | Accessible from anywhere in the program, starts with `$`.                   | `$global_var = 100`       |

---

### **Examples**

#### **Local Variable**
```ruby
def example
  name = "Alice"   # Local variable
  puts name
end
example
```

#### **Instance Variable**
```ruby
class Person
  def initialize(name)
    @name = name    # Instance variable
  end

  def display_name
    puts "Name: #{@name}"
  end
end

person = Person.new("Alice")
person.display_name
```

#### **Class Variable**
```ruby
class Counter
  @@count = 0   # Class variable

  def initialize
    @@count += 1
  end

  def self.current_count
    @@count
  end
end

obj1 = Counter.new
obj2 = Counter.new
puts Counter.current_count   # Output: 2
```

#### **Global Variable**
```ruby
$global_var = "I am global!"   # Global variable

def show_global
  puts $global_var
end

show_global
```

---

## **2. Constants**
Constants သည် Variable ထက်ပိုပြီး Permanent ဖြစ်ပြီး Value ကို သတ်မှတ်ပြီးနောက်မှာ ပြောင်းလဲမရဖို့ ရည်ရွယ်ထားတာဖြစ်တယ်။  
**Syntax**:
- Constants **must start with an uppercase letter**.
- Ruby မှာ Warning ရုံသာပေးပြီး, Constants အတိအကျ ပြောင်းလဲမှုကို ကန့်သတ်မထားပါ။

### **Defining Constants**
```ruby
PI = 3.14159
MAX_ATTEMPTS = 5
```

### **Example: Using Constants**
```ruby
class Circle
  PI = 3.14159

  def self.area(radius)
    PI * radius ** 2
  end
end

puts Circle.area(10)   # Output: 314.159
```

---

## **3. Literals**
Literals ဆိုတာ Data ကို Directly Represent လုပ်တဲ့ Values တွေဖြစ်တယ်။ Ruby မှာ Literals ဟာ Data Type အမျိုးမျိုးကို Represent လုပ်နိုင်တယ်။

### **Common Literals in Ruby**

| **Literal Type**  | **Examples**                                           |
|--------------------|-------------------------------------------------------|
| **Numbers**        | Integer (`42`), Float (`3.14`)                        |
| **Strings**        | `"hello"`, `'world'`                                  |
| **Symbols**        | `:symbol_name`                                        |
| **Arrays**         | `[1, 2, 3]`                                           |
| **Hashes**         | `{ key: "value", age: 25 }`                           |
| **Booleans**       | `true`, `false`                                       |
| **Ranges**         | `(1..5)`                                              |

---

### **Examples of Literals**

#### **Numbers**
```ruby
integer = 42       # Integer literal
float = 3.14       # Float literal
```

#### **Strings**
```ruby
string1 = "Hello, Ruby!"   # Double-quoted string
string2 = 'Hello, World!'  # Single-quoted string
```

#### **Symbols**
Symbols are immutable and used for identifiers.

```ruby
symbol = :my_symbol
puts symbol   # Output: my_symbol
```

#### **Arrays**
```ruby
array = [1, 2, 3, "Ruby", true]
puts array[0]   # Output: 1
```

#### **Hashes**
Hashes store key-value pairs.

```ruby
person = { name: "Alice", age: 25 }
puts person[:name]   # Output: Alice
```

#### **Ranges**
```ruby
range = (1..5)       # Inclusive range
puts range.to_a      # Output: [1, 2, 3, 4, 5]

range_exclusive = (1...5)   # Exclusive range
puts range_exclusive.to_a   # Output: [1, 2, 3, 4]
```

---

## **4. Special Variables**

| **Variable**   | **Description**                                    |
|-----------------|---------------------------------------------------|
| `nil`          | Represents "nothing" or "no value."               |
| `true`, `false`| Boolean literals.                                 |
| `__FILE__`     | Current file name.                                |
| `__LINE__`     | Current line number in the code.                  |

---

### **Special Variables Example**
```ruby
puts __FILE__    # Output: file name
puts __LINE__    # Output: current line number
```

---

## **Summary**
| **Type**        | **Example**                                    |
|------------------|------------------------------------------------|
| Local Variable   | `name = "Ruby"`                               |
| Instance Variable| `@age = 25`                                   |
| Class Variable   | `@@count = 0`                                 |
| Global Variable  | `$global_var = "Global!"`                     |
| Constant         | `PI = 3.142`                                   |
| Literals         | `"Hello"`, `[1, 2, 3]`, `:symbol`, `{}`       |

Ruby Variables, Constants, and Literals သည် Code ရဲ့ Data Store နဲ့ Manipulate လုပ်တာတွေအတွက် အခြေခံအရေးကြီးဆုံး ဖြစ်ပါတယ်။ 😊