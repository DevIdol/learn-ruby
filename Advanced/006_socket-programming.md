### **Ruby - Socket Programming**

Ruby မှာ **Socket programming** သည် network communication များလုပ်ဆောင်ရန် အသုံးပြုသော technique တစ်ခုဖြစ်သည်။ Socket programming က **client-server** model ကို အသုံးပြု၍ data အပြန်အလှန် လွှဲပြောင်းခြင်းကို လုပ်ဆောင်နိုင်ပါသည်။ Ruby မှာ socket programming ကို **`socket`** module ကို အသုံးပြု၍ လွယ်ကူစွာ implement လုပ်နိုင်ပါတယ်။

---

### **1. Socket Programming Overview**

- **Socket** က network connections အတွက် endpoint တစ်ခုဖြစ်ပြီး, **client** နှင့် **server** အကြား data ရွှေ့ပြောင်းခြင်းလုပ်ဆောင်နိုင်ပါသည်။
- Socket programming ကို client-server architecture များတွင် အလွယ်တကူ အသုံးပြုနိုင်သည်။

**Client-Server Model:**
- **Client**: Server နှင့် connection တစ်ခုဖွင့်ပြီး request တစ်ခုပို့ပြီး server မှ response ရယူသည်။
- **Server**: Client ရဲ့ request ကို ဖတ်ပြီး response ပြန်ပေးသည်။

---

### **2. Basic Socket Programming in Ruby**

Ruby မှာ socket programming လုပ်ဖို့အတွက် `socket` module ကို import လုပ်ပြီး socket object တစ်ခု create လုပ်နိုင်ပါတယ်။

#### **2.1. Basic Server Example (TCP Server)**

```ruby
require 'socket'

# Create a server socket that listens on port 2000
server = TCPServer.new('localhost', 2000)

puts "Server is running on localhost:2000"

loop do
  # Wait for a client to connect
  client = server.accept
  puts "Client connected"

  # Send a message to the client
  client.puts "Hello, client!"

  # Receive the message from the client
  message = client.gets.chomp
  puts "Received from client: #{message}"

  # Close the connection
  client.close
  puts "Client disconnected"
end
```

**Explanation:**
- `TCPServer.new('localhost', 2000)` က server socket တစ်ခုကို `localhost` နှင့် port 2000 မှာ ဖွင့်ပါသည်။
- `server.accept` က client တစ်ယောက်၏ connection ကို accept လုပ်ပြီး socket connection တစ်ခု return ပြန်ပါတယ်။
- `client.puts` က client ကို message တစ်ခု ပို့ပါသည်။
- `client.gets.chomp` က client မှထွက်လာသော message ကို receive လုပ်ပါသည်။
- Server သည် client ရဲ့ message ကို print ပြီး connection ကို `client.close` ဖြင့်ပိတ်လိုက်ပါသည်။

---

#### **2.2. Basic Client Example (TCP Client)**

```ruby
require 'socket'

# Connect to the server on localhost, port 2000
client = TCPSocket.new('localhost', 2000)

# Receive the message from the server
message = client.gets.chomp
puts "Received from server: #{message}"

# Send a message to the server
client.puts "Hello, server!"

# Close the connection
client.close
```

**Explanation:**
- `TCPSocket.new('localhost', 2000)` က server အတွက် connection တစ်ခု ဖွင့်သည်။
- `client.gets.chomp` က server မှ ပို့လာသော message ကို ရယူပြီး print ပြသည်။
- `client.puts` က server ကို message တစ်ခု ပို့သည်။
- `client.close` က socket connection ကို close လုပ်သည်။

---

### **3. Working with UDP Sockets**

UDP (User Datagram Protocol) သည် connection-less protocol ဖြစ်ပြီး, client-server architecture မရှိဘဲ data ရွှေ့ပြောင်းနိုင်သော protocol ဖြစ်သည်။ Ruby မှာ UDP socket များကိုလည်း အသုံးပြုနိုင်ပါသည်။

#### **3.1. UDP Server Example**

```ruby
require 'socket'

# Create a UDP socket that listens on port 2000
server = UDPSocket.new
server.bind('localhost', 2000)

puts "UDP Server is running on localhost:2000"

loop do
  # Receive a message from the client
  message, sender = server.recvfrom(1024)
  puts "Received message: #{message} from #{sender}"

  # Send a response back to the client
  server.send("Hello, client!", 0, sender[3], sender[1])
end
```

**Explanation:**
- `UDPSocket.new` က UDP socket object တစ်ခု create လုပ်သည်။
- `server.bind('localhost', 2000)` က server ကို `localhost` မှာ port 2000 တွင် bind လုပ်ပါသည်။
- `server.recvfrom(1024)` က client မှ message ကို receive လုပ်ပါသည်။
- `server.send` က client ကို message တစ်ခု ပြန်ပို့ပါသည်။

#### **3.2. UDP Client Example**

```ruby
require 'socket'

# Create a UDP socket
client = UDPSocket.new

# Send a message to the server
client.send("Hello, server!", 0, 'localhost', 2000)

# Receive a response from the server
message, _ = client.recvfrom(1024)
puts "Received from server: #{message}"

# Close the connection
client.close
```

**Explanation:**
- `UDPSocket.new` က UDP socket object တစ်ခု create လုပ်သည်။
- `client.send("Hello, server!", 0, 'localhost', 2000)` က server ကို message တစ်ခု ပို့ပါသည်။
- `client.recvfrom(1024)` က server မှ response message ကို receive လုပ်ပြီး print ပြပါသည်။

---

### **4. Handling Multiple Clients with Threads**

Server တစ်ခုက client အများအပြားကို handle လုပ်နိုင်ရန် threading ကိုအသုံးပြုနိုင်ပါသည်။ Threading သည် server မှ client အနည်းအများကို concurrently handle လုပ်ရန် အသုံးပြုသော technique တစ်ခုဖြစ်သည်။

#### **4.1. Multi-client Server Example**

```ruby
require 'socket'

server = TCPServer.new('localhost', 2000)
puts "Server is running on localhost:2000"

loop do
  # Accept a client connection and handle it in a new thread
  client = server.accept
  Thread.start(client) do |client_socket|
    client_socket.puts "Hello, client!"
    message = client_socket.gets.chomp
    puts "Received from client: #{message}"
    client_socket.close
  end
end
```

**Explanation:**
- `Thread.start(client)` က client connection တစ်ခုကို thread တစ်ခုတွင် handle လုပ်ပါသည်။ Thread သည် independent အနေနဲ့ client connection များကို concurrently handle လုပ်နိုင်သည်။

---

### **5. Socket Programming Error Handling**

Socket programming တွင် network errors များ ဖြစ်ပေါ်နိုင်ပါသည်။ Ruby မှာ **`begin-rescue`** block ကို error handling အတွက် အသုံးပြုနိုင်ပါတယ်။

#### **5.1. Example of Error Handling in Socket Programming**

```ruby
require 'socket'

begin
  server = TCPServer.new('localhost', 2000)
  puts "Server is running on localhost:2000"

  loop do
    client = server.accept
    client.puts "Hello, client!"
    message = client.gets.chomp
    puts "Received from client: #{message}"
    client.close
  end

rescue => e
  puts "Error occurred: #{e.message}"
ensure
  server.close if server
  puts "Server closed"
end
```

**Explanation:**
- **`begin-rescue`** block သည် socket errors များကို handle လုပ်ရန် အသုံးပြုနိုင်ပါတယ်။
- **`ensure`** block သည် server socket ကို သန့်ရှင်းပေးသည်။

---

Ruby မှာ **Socket programming** ကို TCP နှင့် UDP protocols များအသုံးပြု၍ **client-server communication** ကို အလွယ်တကူ implement လုပ်နိုင်ပါတယ်။ Server-side application တွေကို **`TCPServer`** သို့မဟုတ် **`UDPSocket`** သုံးပြီး socket connection များကို handle လုပ်နိုင်ပြီး, multiple clients ကို **Threading** ဖြင့် concurrent handle လုပ်နိုင်ပါတယ်။ Error handling, multi-client handling နှင့် connection management အတွက် Ruby မှာ အလွယ်တကူ methods များရှိပါသည်။

Socket programming သည် **network-based applications** များ၊ **chat applications** နှင့် **real-time data streaming** အစရှိသည်တို့ကို တည်ဆောက်ရန် အသုံးပြုနိုင်သော အရေးကြီးသော concept ဖြစ်ပါတယ်။