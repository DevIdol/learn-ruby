### **Ruby - Operators**

Ruby သည် Operator-rich Programming Language ဖြစ်ပြီး Data Manipulation နဲ့ Control Structures တွေအတွက် Operators အမျိုးမျိုး ပံ့ပိုးထားပါတယ်။  
Operators တွေဟာ Mathematical Calculations, Comparisons, Logical Operations, နှင့် Data Access တွေမှာ အသုံးပြုနိုင်ပါတယ်။

---

## **1. Arithmetic Operators**
Arithmetic Operators တွေကို Mathematical Operations တွေအတွက် အသုံးပြုသည်။

| **Operator** | **Description**       | **Example**              | **Result**   |
|--------------|-----------------------|--------------------------|--------------|
| `+`          | Addition              | `5 + 3`                  | `8`          |
| `-`          | Subtraction           | `5 - 3`                  | `2`          |
| `*`          | Multiplication        | `5 * 3`                  | `15`         |
| `/`          | Division              | `5 / 2`                  | `2` (integer)|
| `%`          | Modulus (remainder)   | `5 % 2`                  | `1`          |
| `**`         | Exponentiation        | `2 ** 3`                 | `8`          |

---

### **Examples**
```ruby
puts 5 + 3   # Output: 8
puts 5 / 2   # Output: 2 (integer division)
puts 5.0 / 2 # Output: 2.5 (float division)
puts 2 ** 3  # Output: 8
```

---

## **2. Comparison Operators**
Comparison Operators တွေဟာ Data တွေကို တန်းစီဖို့ နှိုင်းယှဉ်မှုတွေအတွက် အသုံးပြုသည်။

| **Operator** | **Description**              | **Example**        | **Result**    |
|--------------|------------------------------|--------------------|---------------|
| `==`         | Equal to                     | `5 == 3`           | `false`       |
| `!=`         | Not equal to                 | `5 != 3`           | `true`        |
| `>`          | Greater than                 | `5 > 3`            | `true`        |
| `<`          | Less than                    | `5 < 3`            | `false`       |
| `>=`         | Greater than or equal to     | `5 >= 3`           | `true`        |
| `<=`         | Less than or equal to        | `5 <= 3`           | `false`       |
| `<=>`        | Combined comparison (spaceship)| `5 <=> 3`         | `1`           |

---

### **Examples**
```ruby
puts 5 == 3   # Output: false
puts 5 <=> 3  # Output: 1 (5 is greater than 3)
puts 3 <=> 5  # Output: -1 (3 is less than 5)
puts 5 <=> 5  # Output: 0 (both are equal)
```

---

## **3. Logical Operators**
Logical Operators တွေကို Conditions တွေကို Combine လုပ်ဖို့ အသုံးပြုသည်။

| **Operator** | **Description**        | **Example**         | **Result**    |
|--------------|------------------------|---------------------|---------------|
| `&&`         | Logical AND            | `true && false`     | `false`       |
| `||`         | Logical OR             | `true || false`     | `true`        |
| `!`          | Logical NOT            | `!true`             | `false`       |
| `and`        | Alternative for `&&`   | `true and false`    | `false`       |
| `or`         | Alternative for `||`   | `true or false`     | `true`        |

---

### **Examples**
```ruby
puts true && false  # Output: false
puts true || false  # Output: true
puts !true          # Output: false
```

---

## **4. Assignment Operators**
Assignment Operators တွေဟာ Variables တွေကို Value သတ်မှတ်ဖို့ သို့မဟုတ် Update လုပ်ဖို့ အသုံးပြုသည်။

| **Operator** | **Description**        | **Example**      | **Result**   |
|--------------|------------------------|------------------|--------------|
| `=`          | Assignment             | `x = 5`          | `x = 5`      |
| `+=`         | Add and assign          | `x += 3`         | `x = x + 3`  |
| `-=`         | Subtract and assign     | `x -= 3`         | `x = x - 3`  |
| `*=`         | Multiply and assign     | `x *= 3`         | `x = x * 3`  |
| `/=`         | Divide and assign       | `x /= 3`         | `x = x / 3`  |
| `%=`         | Modulus and assign      | `x %= 3`         | `x = x % 3`  |

---

### **Examples**
```ruby
x = 5
x += 3   # x = 8
x -= 2   # x = 6
puts x   # Output: 6
```

---

## **5. Bitwise Operators**
Bitwise Operators တွေဟာ Binary Operations တွေအတွက် အသုံးပြုသည်။

| **Operator** | **Description**             | **Example**        | **Result**   |
|--------------|-----------------------------|--------------------|--------------|
| `&`          | AND                         | `5 & 3`            | `1`          |
| `|`          | OR                          | `5 | 3`            | `7`          |
| `^`          | XOR                         | `5 ^ 3`            | `6`          |
| `~`          | Complement                  | `~5`               | `-6`         |
| `<<`         | Left shift                  | `5 << 1`           | `10`         |
| `>>`         | Right shift                 | `5 >> 1`           | `2`          |

---

### **Examples**
```ruby
puts 5 & 3   # Output: 1 (binary AND)
puts 5 | 3   # Output: 7 (binary OR)
puts 5 ^ 3   # Output: 6 (binary XOR)
puts 5 << 1  # Output: 10 (left shift)
```

---

## **6. Range Operators**
Range Operators တွေကို Sequence တိုင်းထွာဖို့ သုံးတယ်။

| **Operator** | **Description**              | **Example**     | **Result**   |
|--------------|------------------------------|-----------------|--------------|
| `..`         | Inclusive range              | `(1..5).to_a`   | `[1, 2, 3, 4, 5]` |
| `...`        | Exclusive range              | `(1...5).to_a`  | `[1, 2, 3, 4]`     |

---

### **Examples**
```ruby
puts (1..5).to_a   # Output: [1, 2, 3, 4, 5]
puts (1...5).to_a  # Output: [1, 2, 3, 4]
```

---

## **7. Ternary Operator**
Ternary Operator ကို Single-line Condition Handling အတွက် သုံးတယ်။

| **Syntax**                   | **Description**               |
|-------------------------------|-------------------------------|
| `condition ? true_case : false_case` | If-else shortcut |

### **Example**
```ruby
x = 5
result = x > 3 ? "Greater" : "Smaller"
puts result   # Output: Greater
```

---

## **8. Defined? Operator**
`defined?` Operator ကို Variable, Method, Class, etc. ရှိမရှိ စစ်ဆေးဖို့ သုံးတယ်။

### **Example**
```ruby
x = 5
puts defined?(x)        # Output: "local-variable"
puts defined?(puts)     # Output: "method"
puts defined?(y)        # Output: nil
```

---

## **9. Logical and Bitwise Differences**
- **Logical Operators**: Used for Boolean conditions.
- **Bitwise Operators**: Work at the binary (bit-level).

---

## **Summary**
Ruby Operators အမျိုးမျိုးသည် Code ကို လွယ်ကူစွာ Manipulate လုပ်ရန် အသုံးဝင်ပြီး, မိမိရဲ့ Logic ကို ထိရောက်စွာ ရေးနိုင်စေတယ်။ 😊