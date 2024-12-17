### **Ruby - Classes and Objects**

Ruby သည် **Pure Object-Oriented Programming Language** ဖြစ်ပြီး အရာဝတ္ထု (Objects) တွေကို အခြေခံထားပါတယ်။ **Class** တွေက အရာဝတ္ထု (Objects) များကို ဖန်တီးဖို့ Template အဖြစ် သုံးတယ်။ Class ထဲမှာ Methods, Variables, Attributes တွေကို သိမ်းဆည်းပြီး, Object တွေကို အခြေခံဖွဲ့စည်းတယ်။

---

## **1. Classes**
Ruby Class က Object တွေကို ဖန်တီးဖို့ Blueprints အဖြစ် သုံးတယ်။  
Class ထဲမှာ Attributes နဲ့ Methods တွေကို သတ်မှတ်နိုင်တယ်။

#### **Class Syntax**
```ruby
class ClassName
  # Define attributes and methods here
end
```

---

## **2. Objects**
Object ဆိုတာ Class တစ်ခုရဲ့ Instance ဖြစ်တယ်။ Object တွေက Data နဲ့ Behavior (Methods) တွေကို ပိုင်ဆိုင်တယ်။

#### **Creating an Object**
```ruby
object = ClassName.new
```

---

## **3. Instance Variables**
Instance Variables ကို `@` Symbol နဲ့သတ်မှတ်တယ်။  
Instance Variable တွေဟာ Object ရဲ့ Data ကို သိမ်းဆည်းတယ်။

---

## **4. Class Example**

#### **Basic Class and Object**
```ruby
class Person
  # Constructor Method
  def initialize(name, age)
    @name = name
    @age = age
  end

  # Instance Method
  def introduce
    puts "Hi, my name is #{@name}, and I am #{@age} years old."
  end
end

# Create an Object
person1 = Person.new("Alice", 25)
person1.introduce   # Output: Hi, my name is Alice, and I am 25 years old.

person2 = Person.new("Bob", 30)
person2.introduce   # Output: Hi, my name is Bob, and I am 30 years old.
```

---

## **5. Attribute Accessors**
Ruby မှာ Attributes ကို **Read/Write** လုပ်ဖို့ Manual Method မရေးချင်ရင် **`attr_accessor`**, **`attr_reader`**, **`attr_writer`** ကိုသုံးတယ်။

#### **Example: Attribute Accessors**
```ruby
class Person
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end
end

person = Person.new("Alice", 25)
puts person.name     # Output: Alice
person.age = 26      # Modify age
puts person.age      # Output: 26
```

| **Attribute**    | **Usage**                                  |
|-------------------|-------------------------------------------|
| `attr_reader`     | Read-only access to attributes            |
| `attr_writer`     | Write-only access to attributes           |
| `attr_accessor`   | Both read and write access to attributes  |

---

## **6. Class Methods**
Class Methods ကို **`self.method_name`** နဲ့သတ်မှတ်တယ်။  
Class Method တွေဟာ Object တစ်ခုကို မဖန်တီးပဲလည်း Call လုပ်နိုင်တယ်။

#### **Example: Class Methods**
```ruby
class Calculator
  def self.add(a, b)
    a + b
  end
end

puts Calculator.add(5, 10)   # Output: 15
```

---

## **7. Inheritance**
Ruby မှာ Class တစ်ခုဟာ **Inheritance** သုံးပြီး Base Class (Parent Class) ရဲ့ Methods, Attributes တွေကို ရယူနိုင်တယ်။

#### **Example: Inheritance**
```ruby
class Animal
  def speak
    puts "I can make a sound!"
  end
end

class Dog < Animal
  def speak
    puts "Woof! Woof!"
  end
end

dog = Dog.new
dog.speak   # Output: Woof! Woof!
```

---

## **8. Overriding Methods**
Subclass မှာ Parent Class ရဲ့ Method ကို Overriding လုပ်ပြီး Behavior ပြောင်းနိုင်တယ်။

#### **Example: Method Overriding**
```ruby
class Parent
  def greet
    puts "Hello from Parent!"
  end
end

class Child < Parent
  def greet
    puts "Hello from Child!"
  end
end

child = Child.new
child.greet   # Output: Hello from Child!
```

---

## **9. Modules as Mixins**
Ruby မှာ **Modules** ကို **Mixin** အဖြစ်သုံးပြီး Code Reusability ကို မြှင့်တင်နိုင်တယ်။ Module ထဲမှာ Define လုပ်ထားတဲ့ Methods တွေကို Class ထဲ Import လုပ်ပြီး အသုံးပြုတယ်။

#### **Example: Mixin**
```ruby
module Greetable
  def greet
    puts "Hello!"
  end
end

class Person
  include Greetable
end

person = Person.new
person.greet   # Output: Hello!
```

---

## **10. Access Control**
Ruby မှာ Methods ကို **Public**, **Private**, **Protected** အဖြစ် Define လုပ်နိုင်တယ်။

| **Access Modifier** | **Description**                                |
|----------------------|-----------------------------------------------|
| `public`            | Accessible from anywhere                     |
| `private`           | Accessible only within the class             |
| `protected`         | Accessible by instances of the same class    |

#### **Example: Access Control**
```ruby
class Person
  def public_method
    puts "I am public!"
  end

  private
  def private_method
    puts "I am private!"
  end
end

person = Person.new
person.public_method        # Output: I am public!
# person.private_method     # Error: private method called
```

---

## **11. Constants**
Class တစ်ခုအတွင်း **Constants** သည် Uppercase Letters ဖြင့် Define လုပ်ရတယ်။

#### **Example: Constants**
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

## **12. Polymorphism**
Polymorphism ဆိုတာ Object တွေဟာ တူညီတဲ့ Method Name ရှိသော်လည်း အပြောင်းအလဲများစွာ နဲ့ Functionality ရေးနိုင်စွမ်းဖြစ်တယ်။

#### **Example: Polymorphism**
```ruby
class Animal
  def speak
    puts "I make a sound!"
  end
end

class Dog < Animal
  def speak
    puts "Woof!"
  end
end

class Cat < Animal
  def speak
    puts "Meow!"
  end
end

animals = [Dog.new, Cat.new]
animals.each { |animal| animal.speak }
# Output:
# Woof!
# Meow!
```

---

## **Summary**
| Feature             | Syntax Example                              |
|----------------------|---------------------------------------------|
| Class Definition     | `class ClassName; end`                     |
| Object Creation      | `object = ClassName.new`                   |
| Instance Variable    | `@variable`                                |
| Attribute Accessors  | `attr_accessor :name`                      |
| Inheritance          | `class Subclass < ParentClass`             |
| Method Overriding    | `def method_name; super; end`              |
| Access Control       | `public`, `private`, `protected`           |
| Constants            | `CONSTANT_NAME = value`                    |

Ruby Classes နှင့် Objects ကို အသုံးပြုပြီး Code ကို Structured, Reusable, Flexible ဖြစ်စေနိုင်ပါတယ်! 😊