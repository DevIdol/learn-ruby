### **Ruby - Object-Oriented Programming (OOP)**

Ruby ဟာ **Object-Oriented Programming (OOP)** ကို အခြေခံထားတဲ့ programming language ဖြစ်ပါတယ်။ OOP အတွက် **class**, **object**, **inheritance**, **polymorphism**, **encapsulation**, **abstraction** စတဲ့ concepts တွေကို Ruby တွင် အသုံးပြုနိုင်ပါတယ်။

Ruby မှာ **everything is an object** ဆိုတာ အဓိပ္ပာယ်က၊ Variable, Methods, Classes စသည်တို့သည် အားလုံး Object များဖြစ်ပြီး၊ Ruby မှာ သုံးတဲ့ အရာတိုင်းသည် Class တွေထဲမှာ ပါဝင်ပါတယ်။ 

---

## **1. Class and Object (class နှင့် object)**

### **1.1 Class**

Ruby မှာ **class** ကို အတိအကျ သတ်မှတ်လိုက်တဲ့ blueprint အနေဖြင့် သုံးပြီး object များကို ဖန်တီးနိုင်ပါတယ်။

```ruby
class Dog
  def speak
    puts "Woof!"
  end
end
```

**Explanation:**
- `class` က အတူတူသော object များ (Dogs) တွေကို ဖန်တီးနိုင်တဲ့ blueprint ဖြစ်ပါတယ်။
- `def` နဲ့ method ကို သတ်မှတ်ပြီး object ရဲ့ behaviors ကို ဖော်ပြပါတယ်။

---

### **1.2 Object**

Object ကို **`new`** method နဲ့ အမှတ်တံဆိပ်ကောင်းတဲ့ class ထဲမှ ဖန်တီးနိုင်ပါတယ်။

```ruby
dog = Dog.new
dog.speak  # Outputs: Woof!
```

**Explanation:**
- `Dog.new` ဟာ `Dog` class ရဲ့ new instance (object) ကို ဖန်တီးပါတယ်။
- `speak` method ကို ရိုက်ပြီး method ရဲ့ result ကို print ထုတ်ပါတယ်။

---

## **2. Instance Variables and Methods**

### **2.1 Instance Variables**
Instance variables ကို class ထဲမှာ `@` ဖြင့် သတ်မှတ်ပါတယ်။

```ruby
class Dog
  def initialize(name)
    @name = name  # Instance variable
  end
  
  def speak
    puts "Woof! My name is #{@name}."
  end
end

dog = Dog.new("Buddy")
dog.speak  # Outputs: Woof! My name is Buddy.
```

**Explanation:**
- `@name` သည် instance variable ဖြစ်ပြီး, object ရဲ့ properties ကို သိမ်းဆည်းထားပါတယ်။
- **`initialize`** method ဟာ object တစ်ခု ဖန်တီးတဲ့အခါ `@name` ကို assign လုပ်ပါတယ်။

---

### **2.2 Instance Methods**

Instance methods တွေက object တစ်ခုရဲ့ behavior ကိုဖော်ပြပါတယ်။

```ruby
class Dog
  def initialize(name)
    @name = name
  end
  
  def speak
    puts "Woof! My name is #{@name}."
  end
end

dog = Dog.new("Max")
dog.speak  # Outputs: Woof! My name is Max.
```

**Explanation:**
- `speak` ဆိုတဲ့ method က `@name` instance variable ကိုအသုံးပြုပြီး object ၏ behavior ကိုပေးသည်။

---

## **3. Class Variables and Methods**

### **3.1 Class Variables**

Class variables ကို `@@` ဖြင့် သတ်မှတ်ပါတယ်။

```ruby
class Dog
  @@total_dogs = 0

  def initialize(name)
    @name = name
    @@total_dogs += 1
  end
  
  def self.total_dogs
    puts "Total dogs: #{@@total_dogs}"
  end
end

dog1 = Dog.new("Buddy")
dog2 = Dog.new("Charlie")

Dog.total_dogs  # Outputs: Total dogs: 2
```

**Explanation:**
- `@@total_dogs` ဟာ class variable ဖြစ်ပြီး၊ class ရဲ့ object တွေက shared သုံးတဲ့ variable ဖြစ်ပါတယ်။
- `self.total_dogs` သည် class method ဖြစ်ပြီး class level တင်သော data ကို access လုပ်နိုင်ပါသည်။

---

### **3.2 Class Methods**

Class method များကို `self` သုံးပြီး သတ်မှတ်ပါတယ်။

```ruby
class Dog
  def self.class_info
    puts "Dogs are loyal pets."
  end
end

Dog.class_info  # Outputs: Dogs are loyal pets.
```

**Explanation:**
- **`self.class_info`** method က class level မှာ သုံးပြီး class ကွဲနေတဲ့ instance များနှင့်ဆိုင်သော data မဟုတ်တဲ့ function ကို define လုပ်တာဖြစ်ပါတယ်။

---

## **4. Inheritance (မွေးဖွားခြင်း)**

Inheritance ဆိုတာ ကလပ်တစ်ခုကနေ အခြားတစ်ခုကို properties (instance variables) နှင့် methods များကို လက်ခံလို့ရတဲ့ feature ဖြစ်ပါတယ်။ Ruby မှာ **`<`** symbol ကို အသုံးပြုပါသည်။

```ruby
class Animal
  def speak
    puts "Animal speaks"
  end
end

class Dog < Animal
  def speak
    puts "Woof!"
  end
end

dog = Dog.new
dog.speak  # Outputs: Woof!
```

**Explanation:**
- `Dog < Animal` ဆိုတာ `Dog` class က `Animal` class ရဲ့ properties များနှင့် methods များကို လက်ခံထားတဲ့ အတိုင်း လုပ်ဆောင်နေပါသည်။
- `Dog` class မှာ `speak` method ကို overwrite လုပ်ထားပြီး၊ `Dog` က အဲဒီ `speak` method ကို အသုံးပြုနေပါသည်။

---

## **5. Polymorphism (မျိုးစုံလိုက်ဖက်မှု)**

Polymorphism ဆိုတာ **same method name** ကို different classes တွေမှာ **different implementations** ရှိတတ်တဲ့ feature ဖြစ်ပါတယ်။

```ruby
class Dog
  def speak
    puts "Woof!"
  end
end

class Cat
  def speak
    puts "Meow!"
  end
end

def make_sound(animal)
  animal.speak
end

dog = Dog.new
cat = Cat.new

make_sound(dog)  # Outputs: Woof!
make_sound(cat)  # Outputs: Meow!
```

**Explanation:**
- `Dog` နှင့် `Cat` class တို့မှာ `speak` method ဟာ method name တူကြောင်း၊ သို့သော် အပြုအမူမှာ ကွဲပြားနေပါသည်။
- **`make_sound`** method က polymorphic method ဖြစ်ပြီး၊ ဘယ် class မှာရှိတဲ့ object မဆို `speak` method ကို ကွဲပြားစွာသုံးနိုင်ပါတယ်။

---

## **6. Encapsulation (ဝှက်ခြင်း)**

Encapsulation ဆိုတာ Object ရဲ့ data (instance variables) ကို **private** နေရာမှာ ဖျက်ပစ်ပြီး public methods အကယ်၍ ခေါ်ယူသုံးဖို့ထားပေးတဲ့ concept ဖြစ်ပါတယ်။

```ruby
class BankAccount
  def initialize(balance)
    @balance = balance
  end

  def deposit(amount)
    @balance += amount
  end

  def withdraw(amount)
    @balance -= amount if amount <= @balance
  end

  def display_balance
    puts "Your balance is $#{@balance}"
  end
end

account = BankAccount.new(100)
account.deposit(50)
account.withdraw(30)
account.display_balance  # Outputs: Your balance is $120
```

**Explanation:**
- `@balance` instance variable ကို **direct access** မပေးပါဘူး။ `deposit`, `withdraw` methods အားဖြင့်သာ update လုပ်နိုင်ပါတယ်။

---

## **7. Abstraction (ပြသခြင်း)**

Abstraction ဆိုတာ အရေးကြီးသော detail များကို hide လုပ်ပြီး, အရေးပါသော functionality ပေါ်မှာသာ focus လုပ်ခြင်းဖြစ်ပါတယ်။

```ruby
class Car
  def initialize(make, model)
    @make = make
    @model = model
  end

  def start_engine
    puts "Starting the engine of #{@make} #{@model}."
  end
end

car = Car.new("Toyota", "Corolla")
car.start_engine  # Outputs: Starting the engine of Toyota Corolla.
```

**Explanation:**
- `Car` class မှာ အင်ဂျင်စတင်ရန်အသုံးပြုတဲ့ method ကို define လုပ်ထားပြီး car object ရဲ့ details ကို abstraction ပေးထားသည်။

---

## **Conclusion**

Ruby မှာ Object-Oriented Programming (OOP) ၏ core concepts များကို **class**, **object**, **inheritance**, **polymorphism**, **encapsulation**, **abstraction** စသည်ဖြင့် အသုံးပြုနိုင်ပါတယ်။ Ruby ရဲ့ OOP ဟာ code maintainability ကို မြှင့်တင်ပေးပြီး, Reusability နှင့် Modularity ကိုအလွယ်တကူပေးပါတယ်။