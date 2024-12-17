### **Ruby - Strings**

Ruby မှာ **Strings** ဟာ Text Data ကို Represent လုပ်ဖို့ အသုံးပြုပါတယ်။ String ဆိုတာ Character (စာလုံး) အစုတစ်စု ဖြစ်ပြီး Single Quotes (`'`) သို့မဟုတ် Double Quotes (`"`) ကို သုံးပြီး Define လုပ်တယ်။

---

## **1. Creating Strings**
Ruby မှာ String တွေကို Multiple Formats နဲ့ Create လုပ်နိုင်တယ်။

### **1.1 Single Quotes**
- Single Quotes သုံးပြီး Create လုပ်လို့ရတယ်။  
- Escape Characters (`\`) ကို Support မလုပ်ဘဲ Plain Text အဖြစ်မှတ်တယ်။
```ruby
string = 'Hello, Ruby!'
puts string  # Output: Hello, Ruby!
```

---

### **1.2 Double Quotes**
- Double Quotes သုံးလျှင် String Interpolation နဲ့ Escape Characters (`\n`, `\t`) ကို Support လုပ်တယ်။
```ruby
string = "Hello, Ruby!\nWelcome to Strings."
puts string
# Output:
# Hello, Ruby!
# Welcome to Strings.
```

---

### **1.3 String Interpolation**
- Double Quotes ထဲမှာ **`#{}`** ကိုသုံးပြီး Variables သို့မဟုတ် Expressions တွေကို Embed လုပ်နိုင်တယ်။
```ruby
name = "Alice"
puts "Hello, #{name}!"  # Output: Hello, Alice!
puts "2 + 2 = #{2 + 2}" # Output: 2 + 2 = 4
```

---

### **1.4 Multiline Strings**
- **`%Q`** သို့မဟုတ် Here Document (`<<-`) ကို အသုံးပြုပြီး Multiline Strings ရေးနိုင်တယ်။

#### **Using `%Q`**
```ruby
string = %Q{
This is a multiline
string in Ruby.
}
puts string
```

#### **Using Here Document**
```ruby
string = <<-TEXT
This is another
multiline string.
TEXT
puts string
```

---

## **2. Common String Methods**
Ruby မှာ Strings နဲ့ အလုပ်လုပ်ဖို့ အတွက် Useful Methods အများကြီး ပါတယ်။

---

### **2.1 Concatenation**
String တွေကို **`+`** သို့မဟုတ် **`<<`** နဲ့ ပေါင်းနိုင်တယ်။
```ruby
string1 = "Hello"
string2 = "World"
puts string1 + " " + string2  # Output: Hello World
puts string1 << " Ruby!"      # Output: Hello Ruby!
```

---

### **2.2 Repetition**
**`*`** Operator ကိုသုံးပြီး String ကို အကြိမ်ကြိမ် ထပ်ပေါင်းနိုင်တယ်။
```ruby
puts "Ruby! " * 3  # Output: Ruby! Ruby! Ruby!
```

---

### **2.3 String Length**
**`length`** သို့မဟုတ် **`size`** Method ကို သုံးပြီး String Length ကို ရနိုင်တယ်။
```ruby
string = "Hello, Ruby!"
puts string.length  # Output: 12
puts string.size    # Output: 12
```

---

### **2.4 Changing Case**
```ruby
string = "Ruby Programming"
puts string.upcase   # Output: RUBY PROGRAMMING
puts string.downcase # Output: ruby programming
puts string.capitalize # Output: Ruby programming
puts string.swapcase # Output: rUBY pROGRAMMING
```

---

### **2.5 Substrings**
**`[]`** ကိုသုံးပြီး Substring ကို ရယူနိုင်တယ်။
```ruby
string = "Hello, Ruby!"
puts string[0]       # Output: H
puts string[0, 5]    # Output: Hello (Start at 0, length 5)
puts string[-4..-1]  # Output: Ruby
```

---

### **2.6 Searching Strings**
- **`include?`**: String တစ်ခုပါရှိမရှိစစ်တယ်။
- **`index`**: String ရဲ့ Starting Index ကို Return ပြန်တယ်။
```ruby
string = "Hello, Ruby!"
puts string.include?("Ruby")  # Output: true
puts string.index("Ruby")     # Output: 7
```

---

### **2.7 Replacing Strings**
- **`sub`**: Replace the first occurrence of a pattern.
- **`gsub`**: Replace all occurrences of a pattern.
```ruby
string = "Ruby is fun. Ruby is powerful."
puts string.sub("Ruby", "Python")  # Output: Python is fun. Ruby is powerful.
puts string.gsub("Ruby", "Python") # Output: Python is fun. Python is powerful.
```

---

### **2.8 Splitting and Joining Strings**
- **`split`**: Split a string into an array.
- **`join`**: Join an array into a string.
```ruby
string = "Ruby,Python,Java"
languages = string.split(",")
puts languages.inspect  # Output: ["Ruby", "Python", "Java"]

joined_string = languages.join(" | ")
puts joined_string  # Output: Ruby | Python | Java
```

---

### **2.9 Stripping Whitespace**
**`strip`**, **`lstrip`**, and **`rstrip`** are used to remove extra spaces.
```ruby
string = "   Ruby Programming   "
puts string.strip  # Output: Ruby Programming
puts string.lstrip # Output: Ruby Programming   
puts string.rstrip # Output:    Ruby Programming
```

---

## **3. String Comparison**
Strings can be compared using the following operators:
- **`==`**: Checks equality.
- **`<, >, <=, >=`**: Lexicographical comparison.
- **`eql?`**: Strict equality check.

### **Example**
```ruby
puts "Ruby" == "Ruby"  # Output: true
puts "A" < "B"         # Output: true
puts "Ruby".eql?("Ruby") # Output: true
```

---

## **4. Special Characters**
- **`\n`**: Newline.
- **`\t`**: Tab.
- **`\\`**: Backslash.
- **`\"`**: Double quote.

### **Example**
```ruby
puts "Hello\nWorld" # Output:
# Hello
# World
```

---

## **5. String Encoding**
Ruby Strings support different encodings.  
Use **`encoding`** to check or change encoding.
```ruby
string = "Hello, Ruby!"
puts string.encoding  # Output: UTF-8
```

---

## **6. Frozen Strings**
String literals can be made immutable using **`freeze`**.
```ruby
string = "Hello".freeze
# string << " World"  # Error: can't modify frozen String
```

---

## **7. Summary Table**

| **Method**         | **Description**                                     | **Example**                      |
|--------------------|-----------------------------------------------------|----------------------------------|
| `length`/`size`    | Get the length of the string                        | `"Ruby".length`                 |
| `upcase`/`downcase`| Convert to uppercase or lowercase                   | `"ruby".upcase`                 |
| `sub`/`gsub`       | Replace part/all of a string                        | `"Ruby".sub("u", "a")`          |
| `split`/`join`     | Split into array or join array into string          | `"a,b".split(",")`              |
| `include?`         | Check if a substring exists                         | `"Ruby".include?("R")`          |
| `strip`/`lstrip`   | Remove leading/trailing whitespace                  | `"  Ruby  ".strip`              |
| `*`                | Repeat the string                                   | `"Ruby " * 3`                   |
| `<<`               | Append to string                                    | `"Hello" << " World"`           |

---

Ruby Strings တွေဟာ Powerful Features တွေ Support လုပ်ပေးပြီး Flexible Text Processing အတွက် အထူးသင့်လျော်ပါတယ်။ 😊