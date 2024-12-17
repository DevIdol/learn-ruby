### **Ruby - Hashes**

Ruby မှာ **Hash** ဆိုတာ Key-Value Pair တွေကို သိမ်းဆည်းဖို့ အသုံးပြုတဲ့ Data Structure တစ်ခု ဖြစ်ပါတယ်။ Hashes ဟာ Data ကို Key (Unique Identifier) အပေါ်မူတည်ပြီး Store လုပ်ပြီး Access လုပ်နိုင်အောင် ဖန်တီးထားပါတယ်။

---

## **1. Creating Hashes**

### **1.1 Using Curly Braces (`{}`)**
```ruby
# Creating a hash
hash = { "name" => "Alice", "age" => 25, "city" => "New York" }
puts hash.inspect
# Output: {"name"=>"Alice", "age"=>25, "city"=>"New York"}
```

### **1.2 Using `Hash.new`**
```ruby
# Creating an empty hash
hash = Hash.new
puts hash.inspect  # Output: {}

# Default value for missing keys
hash = Hash.new("default value")
puts hash[:missing_key] # Output: default value
```

### **1.3 Symbol Keys**
- Common practice is to use Symbols (`:key`) as keys in Hashes for efficiency.
```ruby
hash = { name: "Alice", age: 25, city: "New York" }
puts hash.inspect
# Output: {:name=>"Alice", :age=>25, :city=>"New York"}
```

---

## **2. Accessing Hash Values**

### **2.1 Using Keys**
```ruby
hash = { name: "Alice", age: 25 }
puts hash[:name] # Output: Alice
puts hash[:age]  # Output: 25
```

### **2.2 Using `fetch`**
- Safely fetches a value with the option to provide a default or raise an error if the key doesn’t exist.
```ruby
hash = { name: "Alice" }
puts hash.fetch(:name, "Unknown") # Output: Alice
puts hash.fetch(:city, "Unknown") # Output: Unknown
```

---

## **3. Adding and Modifying Entries**

### **3.1 Adding New Pairs**
```ruby
hash = { name: "Alice" }
hash[:age] = 25
puts hash.inspect # Output: {:name=>"Alice", :age=>25}
```

### **3.2 Updating Existing Values**
```ruby
hash = { name: "Alice", age: 25 }
hash[:age] = 30
puts hash.inspect # Output: {:name=>"Alice", :age=>30}
```

---

## **4. Removing Entries**

### **4.1 Using `delete`**
```ruby
hash = { name: "Alice", age: 25 }
hash.delete(:age)
puts hash.inspect # Output: {:name=>"Alice"}
```

### **4.2 Using `delete_if`**
- Removes key-value pairs based on a condition.
```ruby
hash = { name: "Alice", age: 25, city: "New York" }
hash.delete_if { |key, value| key == :age }
puts hash.inspect # Output: {:name=>"Alice", :city=>"New York"}
```

---

## **5. Iterating Through Hashes**

### **5.1 Using `each`**
```ruby
hash = { name: "Alice", age: 25 }
hash.each do |key, value|
  puts "#{key}: #{value}"
end
# Output:
# name: Alice
# age: 25
```

### **5.2 Using `each_key` and `each_value`**
```ruby
hash = { name: "Alice", age: 25 }
hash.each_key { |key| puts key }    # Output: name, age
hash.each_value { |value| puts value } # Output: Alice, 25
```

---

## **6. Common Hash Methods**

### **6.1 Checking for Keys or Values**
- **`key?`** or **`has_key?`**: Checks if a key exists.
- **`value?`** or **`has_value?`**: Checks if a value exists.
```ruby
hash = { name: "Alice", age: 25 }
puts hash.key?(:name)      # Output: true
puts hash.value?(25)       # Output: true
```

### **6.2 Merging Hashes**
- **`merge`**: Combines two hashes into a new hash.
```ruby
hash1 = { name: "Alice" }
hash2 = { age: 25 }
merged = hash1.merge(hash2)
puts merged.inspect # Output: {:name=>"Alice", :age=>25}
```

### **6.3 Getting Keys and Values**
- **`keys`**: Returns all keys as an array.
- **`values`**: Returns all values as an array.
```ruby
hash = { name: "Alice", age: 25 }
puts hash.keys.inspect   # Output: [:name, :age]
puts hash.values.inspect # Output: ["Alice", 25]
```

---

## **7. Hashes as Parameters**

Hashes are commonly used in Ruby methods as arguments for optional parameters.

```ruby
def greet(options = {})
  name = options[:name] || "Guest"
  age = options[:age] || "unknown"
  puts "Hello #{name}, age #{age}!"
end

greet(name: "Alice", age: 25) # Output: Hello Alice, age 25!
greet                         # Output: Hello Guest, age unknown!
```

---

## **8. Hash Transformations**

### **8.1 Transforming Keys**
```ruby
hash = { "name" => "Alice", "age" => 25 }
symbolized_hash = hash.transform_keys(&:to_sym)
puts symbolized_hash.inspect # Output: {:name=>"Alice", :age=>25}
```

### **8.2 Transforming Values**
```ruby
hash = { name: "Alice", age: 25 }
uppercase_values = hash.transform_values(&:to_s)
puts uppercase_values.inspect # Output: {:name=>"Alice", :age=>"25"}
```

---

## **9. Default Values**

### **9.1 Setting Default Values**
If a key is missing, a default value can be returned.
```ruby
hash = Hash.new("default")
puts hash[:missing] # Output: default
```

### **9.2 Using Blocks**
```ruby
hash = Hash.new { |hash, key| hash[key] = "Value for #{key}" }
puts hash[:name] # Output: Value for name
puts hash.inspect # Output: {:name=>"Value for name"}
```

---

## **10. Nested Hashes**

Hashes can be nested to represent complex data structures.
```ruby
nested_hash = {
  user: {
    name: "Alice",
    address: {
      city: "New York",
      zip: "10001"
    }
  }
}
puts nested_hash[:user][:address][:city] # Output: New York
```

---

## **11. Summary Table**

| **Method**          | **Description**                                     | **Example**                      |
|---------------------|-----------------------------------------------------|----------------------------------|
| `key?`/`has_key?`   | Checks if a key exists                              | `hash.key?(:key)`               |
| `value?`/`has_value?`| Checks if a value exists                           | `hash.value?(value)`            |
| `merge`             | Combines two hashes                                | `hash1.merge(hash2)`            |
| `each`              | Iterate over key-value pairs                       | `hash.each { |k, v| ... }`      |
| `delete`            | Removes a key-value pair                           | `hash.delete(:key)`             |
| `transform_keys`    | Transforms keys                                     | `hash.transform_keys(&:to_sym)` |
| `transform_values`  | Transforms values                                   | `hash.transform_values(&:upcase)` |
| `default`           | Sets a default value for missing keys              | `hash.default = "value"`        |

---

Ruby Hashes ဟာ Flexible ဖြစ်ပြီး Key-Value Data ကို Manage လုပ်ရာမှာ အထူးအဆင်ပြေပါတယ်! 😊