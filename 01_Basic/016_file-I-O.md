### **Ruby - File I/O (Input/Output)**

Ruby မှာ File I/O (Input/Output) ကို Handle လုပ်ဖို့အတွက် လွယ်ကူတဲ့ Methods တွေပါရှိပြီး File Reading, Writing, Deleting နဲ့ Manipulating လုပ်နိုင်ပါတယ်။

---

## **1. File Operations မိတ်ဆက်**

Ruby မှာ File I/O ကို Handle လုပ်တဲ့ Built-in **`File`** Class နဲ့ **`IO`** Class တွေပါရှိတယ်။ File I/O ကိုသုံးပြီး ဖိုင်များကို ဖန်တီး, ဖတ်, ပြင်ဆင်, ဖျက်နိုင်ပါတယ်။

---

## **2. File Reading (ဖိုင်ဖတ်ခြင်း)**

### **2.1 Reading the Entire File**
**`File.read`** Method ကို File ထဲမှာရှိတဲ့ Content အားလုံးကို ဖတ်ဖို့အသုံးပြုပါတယ်။
```ruby
# sample.txt file ကို ဖတ်မယ်
content = File.read("sample.txt")
puts content
```

---

### **2.2 Reading Line by Line**
**`File.foreach`** Method ကို File ကို Line by Line ဖတ်ဖို့ အသုံးပြုနိုင်ပါတယ်။
```ruby
File.foreach("sample.txt") do |line|
  puts line
end
```

---

### **2.3 Open and Read**
**`File.open`** ကို ဖိုင်ကို ဖွင့်ပြီး Content ဖတ်ဖို့အသုံးပြုတယ်။
```ruby
File.open("sample.txt", "r") do |file|
  while line = file.gets
    puts line
  end
end
```

---

## **3. File Writing (ဖိုင်ရေးခြင်း)**

### **3.1 Writing to a File (Overwrite)**
**`File.write`** ကို ဖိုင်ထဲမှာ Content အသစ်ရေးမယ် (Overwrite လုပ်တယ်)။
```ruby
File.write("output.txt", "Hello, Ruby File I/O!")
# output.txt ထဲမှာ "Hello, Ruby File I/O!" ရေးထားလိမ့်မယ်။
```

---

### **3.2 Appending to a File (Content ချိတ်ဆက်ရေးခြင်း)**
**`File.open`** Method ကို **`"a"`** Mode နဲ့ ဖိုင်မှာ Content ချိတ်ဆက်ရေးဖို့ အသုံးပြုနိုင်ပါတယ်။
```ruby
File.open("output.txt", "a") do |file|
  file.puts "Appending this line to the file."
end
```

---

## **4. File Modes**

File ကို ဖွင့်တဲ့အခါ အောက်ပါ Modes တွေကို သတ်မှတ်နိုင်ပါတယ်။

| **Mode** | **Description**                   |
|----------|-----------------------------------|
| `"r"`    | Read-Only Mode                    |
| `"w"`    | Write Mode (Overwrite Content)    |
| `"a"`    | Append Mode (Add Content)         |
| `"r+"`   | Read and Write Mode               |
| `"w+"`   | Read and Write (Overwrite)        |
| `"a+"`   | Read and Write (Append)           |

---

## **5. File Existence and Metadata**

### **5.1 Check if File Exists**
**`File.exist?`** Method ကို ဖိုင်ရှိမရှိစစ်မယ်။
```ruby
puts File.exist?("sample.txt")  # true or false
```

---

### **5.2 Get File Information**
```ruby
puts File.size("sample.txt")       # File Size
puts File.basename("sample.txt")   # File Name
puts File.dirname("sample.txt")    # Directory Name
puts File.extname("sample.txt")    # File Extension
```

---

## **6. Deleting Files**

**`File.delete`** Method ကို ဖိုင်ကို ဖျက်ဖို့အသုံးပြုပါတယ်။
```ruby
File.delete("output.txt") if File.exist?("output.txt")
```

---

## **7. File Handling Best Practices**

File Handling လုပ်တဲ့အခါ Error Handling ကို ထည့်သွင်းစဉ်းစားရမယ်။

### **7.1 Using `begin...rescue...ensure`**
```ruby
begin
  File.open("sample.txt", "r") do |file|
    puts file.read
  end
rescue Errno::ENOENT => e
  puts "File not found: #{e.message}"
ensure
  puts "File handling complete."
end
```

---

## **8. Directory Handling**

Ruby မှာ Directories ကို Manage လုပ်ဖို့အတွက် **`Dir`** Class ကို အသုံးပြုတယ်။

### **8.1 List All Files in a Directory**
```ruby
Dir.foreach(".") do |file|
  puts file
end
```

### **8.2 Create a Directory**
```ruby
Dir.mkdir("new_folder") unless Dir.exist?("new_folder")
```

### **8.3 Delete a Directory**
```ruby
Dir.rmdir("new_folder") if Dir.exist?("new_folder")
```

---

## **9. Example Code**

### **9.1 Reading and Writing Example**
```ruby
# Write content to a file
File.write("example.txt", "This is Ruby File I/O example!")

# Read and display content
content = File.read("example.txt")
puts "File Content: #{content}"
```

---

## **10. Summary Table**

| **Action**              | **Code**                                | **Example**                          |
|-------------------------|------------------------------------------|--------------------------------------|
| Read File               | `File.read("file.txt")`                 | Entire file content                 |
| Read Line by Line       | `File.foreach("file.txt") { |line| }`    | Line-by-line reading                |
| Write File (Overwrite)  | `File.write("file.txt", "content")`      | Replace content                     |
| Append to File          | `File.open("file.txt", "a") { |f| }`     | Add new content                     |
| Check File Existence    | `File.exist?("file.txt")`               | true/false                          |
| Get File Size           | `File.size("file.txt")`                 | File size in bytes                  |
| Delete File             | `File.delete("file.txt")`               | Remove file                         |
| Create Directory        | `Dir.mkdir("dir_name")`                 | Make a new folder                   |
| List Files in Directory | `Dir.foreach(".")`                      | Display all files in current dir    |

---

Ruby ရဲ့ File I/O ဟာ File System ကို Manage လုပ်ဖို့အတွက် Flexible ဖြစ်တဲ့ Tools တွေကို ပေးထားတာမို့ နေ့စဉ် Programming Tasks တွေမှာ အလွယ်တကူ အသုံးပြုနိုင်ပါတယ်။ 😊