### **Ruby - Arrays**

Ruby မှာ **Arrays** ဟာ Data Items တွေကို **Ordered Collection** အဖြစ် သိမ်းဆည်းရာတွင် အသုံးပြုပါတယ်။ Arrays တွေဟာ Heterogeneous ဖြစ်ပြီး Data Types မျိုးစုံကို တစ်ခုတည်းသော Array ထဲမှာ တူတူ သိမ်းဆည်းနိုင်ပါတယ်။ Indexing အပေါ်မှာ အခြေခံပြီး Access လုပ်နိုင်ပါတယ်။

---

## **1. Creating Arrays**

### **1.1 Using Square Brackets (`[]`)**
```ruby
# Creating an array
array = [1, 2, 3, "Ruby", true]
puts array.inspect
# Output: [1, 2, 3, "Ruby", true]
```

### **1.2 Using `Array.new`**
```ruby
# Empty array
empty_array = Array.new
puts empty_array.inspect # Output: []

# Array with default size and values
array_with_defaults = Array.new(3, "default")
puts array_with_defaults.inspect
# Output: ["default", "default", "default"]
```

---

## **2. Accessing Elements**

### **2.1 Using Index**
Ruby Arrays use zero-based indexing.  
Negative indexes start from the end of the array.
```ruby
array = ["Ruby", "Python", "Java"]

puts array[0]  # Output: Ruby
puts array[-1] # Output: Java
```

### **2.2 Accessing Ranges**
Use range operators (`..` or `...`) to retrieve a subarray.
```ruby
array = [1, 2, 3, 4, 5]

puts array[1..3].inspect # Output: [2, 3, 4]
puts array[1...3].inspect # Output: [2, 3]
```

---

## **3. Modifying Arrays**

### **3.1 Adding Elements**
- **`push`** or **`<<`**: Add elements to the end.
- **`unshift`**: Add elements to the beginning.
```ruby
array = [1, 2, 3]
array.push(4)        # [1, 2, 3, 4]
array << 5           # [1, 2, 3, 4, 5]
array.unshift(0)     # [0, 1, 2, 3, 4, 5]
puts array.inspect
```

### **3.2 Removing Elements**
- **`pop`**: Removes the last element.
- **`shift`**: Removes the first element.
```ruby
array = [1, 2, 3]
array.pop     # [1, 2]
array.shift   # [2]
puts array.inspect
```

### **3.3 Deleting Specific Elements**
- **`delete`**: Remove elements matching a value.
- **`delete_at`**: Remove elements by index.
```ruby
array = [1, 2, 3, 2]
array.delete(2)      # [1, 3]
array = [1, 2, 3]
array.delete_at(1)   # [1, 3]
puts array.inspect
```

---

## **4. Iterating Over Arrays**

### **4.1 Using `each`**
```ruby
array = [1, 2, 3]
array.each { |item| puts item }
# Output:
# 1
# 2
# 3
```

### **4.2 Using `map`**
- Returns a new array with the results of the block.
```ruby
array = [1, 2, 3]
squared = array.map { |num| num * num }
puts squared.inspect # Output: [1, 4, 9]
```

---

## **5. Common Array Methods**

### **5.1 Checking Membership**
- **`include?`**: Check if an element exists.
```ruby
array = [1, 2, 3]
puts array.include?(2) # Output: true
```

### **5.2 Sorting**
- **`sort`**: Returns a sorted array.
- **`reverse`**: Reverses the array order.
```ruby
array = [3, 1, 2]
puts array.sort.inspect   # Output: [1, 2, 3]
puts array.reverse.inspect # Output: [2, 1, 3]
```

### **5.3 Getting Unique Elements**
- **`uniq`**: Removes duplicate elements.
```ruby
array = [1, 2, 2, 3, 3]
puts array.uniq.inspect # Output: [1, 2, 3]
```

### **5.4 Combining Arrays**
- **`+`**: Concatenate arrays.
- **`|`**: Union of arrays (removes duplicates).
```ruby
array1 = [1, 2]
array2 = [2, 3]
puts (array1 + array2).inspect # Output: [1, 2, 2, 3]
puts (array1 | array2).inspect # Output: [1, 2, 3]
```

### **5.5 Finding Intersection**
- **`&`**: Returns common elements.
```ruby
array1 = [1, 2, 3]
array2 = [2, 3, 4]
puts (array1 & array2).inspect # Output: [2, 3]
```

---

## **6. Multidimensional Arrays**
Ruby supports nested arrays.
```ruby
matrix = [[1, 2], [3, 4]]
puts matrix[0][1] # Output: 2
```

---

## **7. Array Conversion**
Convert other data types to arrays.
```ruby
string = "Ruby"
puts string.chars.inspect  # Output: ["R", "u", "b", "y"]

range = (1..3)
puts range.to_a.inspect    # Output: [1, 2, 3]
```

---

## **8. Array Length**
Use **`length`** or **`size`**.
```ruby
array = [1, 2, 3]
puts array.length # Output: 3
```

---

## **9. Summary Table**

| **Method**          | **Description**                            | **Example**                         |
|---------------------|--------------------------------------------|-------------------------------------|
| `push`/`<<`         | Add elements to the end                   | `array.push(1)`                    |
| `unshift`           | Add elements to the beginning             | `array.unshift(1)`                 |
| `pop`               | Remove and return the last element        | `array.pop`                        |
| `shift`             | Remove and return the first element       | `array.shift`                      |
| `include?`          | Check if an element exists                | `array.include?(value)`            |
| `sort`              | Return sorted array                      | `array.sort`                       |
| `uniq`              | Remove duplicate elements                | `array.uniq`                       |
| `map`               | Transform each element                   | `array.map { |x| x * x }`          |
| `each`              | Iterate over elements                    | `array.each { |x| puts x }`        |
| `&`                 | Intersection of two arrays               | `array1 & array2`                  |
| `|`                 | Union of two arrays                      | `array1 | array2`                  |

---

Ruby Arrays are **powerful** and **versatile**, making them suitable for a wide range of data manipulation tasks! 😊