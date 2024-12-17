### **Ruby - XML, XSLT, and XPath Tutorial**

Ruby မှာ **XML (Extensible Markup Language)**, **XSLT (Extensible Stylesheet Language Transformations)** နှင့် **XPath (XML Path Language)** ကို အသုံးပြု၍ XML data များကို read, manipulate, transform လုပ်နိုင်ပါတယ်။ Ruby တွင် **xml/libxml** သို့မဟုတ် **nokogiri** gem များကို အသုံးပြုလို့ ရပါတယ်။

ဒီ tutorial တွင် **XML**, **XSLT** နှင့် **XPath** အကြောင်းကို **Ruby** တွင်ဘယ်လိုအသုံးပြုမလဲဆိုတာကို ရှင်းပြပါမယ်။

---

### **1. Working with XML in Ruby**

**XML (Extensible Markup Language)** သည် data ကို structured format ဖြင့် ဖော်ပြနိုင်သော markup language တစ်ခု ဖြစ်သည်။ XML သည် element-based structure ဖြစ်ပြီး, tags များဖြင့် data တွေကို ဖော်ပြပေးသည်။

Ruby တွင် XML ဖိုင်များကို handle လုပ်ရန် **Nokogiri** gem သို့မဟုတ် **REXML** gem ကို အသုံးပြုနိုင်ပါတယ်။ ဒါ့အပြင် **Nokogiri** သည် XML ကို parse လုပ်ခြင်း, XPath query များ running လုပ်ခြင်းနှင့် XSLT transformations လုပ်ခြင်းတို့အတွက် အလွန်အသုံးဝင်သော gem ဖြစ်ပါတယ်။

---

#### **1.1. Parsing XML with Nokogiri**

**Nokogiri** gem သည် Ruby တွင် XML ကို parsing လုပ်ရာမှာ အသုံးပြုနိုင်သော library ဖြစ်သည်။ **Nokogiri** ကို install လုပ်ရန်:

```bash
gem install nokogiri
```

XML data ကို parsing လုပ်နည်း:

```ruby
require 'nokogiri'
require 'open-uri'

# Sample XML data (from a file or string)
xml_data = <<-XML
<bookstore>
  <book>
    <title lang="en">Programming Ruby</title>
    <author>David Flanagan</author>
    <price>39.95</price>
  </book>
  <book>
    <title lang="es">Ruby para Principiantes</title>
    <author>Marcelo de Moraes</author>
    <price>29.95</price>
  </book>
</bookstore>
XML

# Parse the XML data
doc = Nokogiri::XML(xml_data)

# Accessing elements
doc.xpath('//book/title').each do |title|
  puts "Title: #{title.text}"
end
```

**Explanation:**
- **`Nokogiri::XML(xml_data)`** သည် XML data ကို parse လုပ်ပြီး document object model (DOM) တစ်ခု ပြန်လည်ပြုလုပ်ပေးသည်။
- **`xpath('//book/title')`** က XPath query အသုံးပြုပြီး `book` element အတွင်းရှိ `title` element များကို ရယူသည်။

---

### **2. Working with XPath in Ruby**

**XPath** သည် XML document ထဲမှ elements များကို ရှာဖွေရန် သုံးသော language တစ်ခု ဖြစ်သည်။ **XPath** သည် elements များကို location path ဖြင့် ရှာဖွေရန် အသုံးပြုသည်။ Ruby တွင် **Nokogiri** gem သည် XPath query များကို support လုပ်ပါသည်။

#### **2.1. Using XPath Queries**

```ruby
require 'nokogiri'

xml_data = <<-XML
<bookstore>
  <book>
    <title lang="en">Ruby Programming</title>
    <author>David Flanagan</author>
    <price>39.95</price>
  </book>
  <book>
    <title lang="es">Programación en Ruby</title>
    <author>Marcelo de Moraes</author>
    <price>29.95</price>
  </book>
</bookstore>
XML

doc = Nokogiri::XML(xml_data)

# XPath query to get all titles in the XML document
doc.xpath('//book/title').each do |title|
  puts "Title: #{title.text}, Language: #{title['lang']}"
end
```

**Explanation:**
- **`//book/title`** သည် XPath query ဖြစ်ပြီး, document မှာရှိတဲ့ `book` element အတွင်းရှိ `title` element များအားလုံးကို ရှာဖွေသည်။
- `title['lang']` က `title` element ၏ `lang` attribute ကို ရယူသည်။

---

### **3. XSLT Transformations in Ruby**

**XSLT (Extensible Stylesheet Language Transformations)** သည် XML document ကို transform လုပ်ရန် အသုံးပြုသော language တစ်ခုဖြစ်သည်။ XSLT ကို အသုံးပြုပြီး XML ကို အခြား format များ (HTML, Text, etc.) အဖြစ်ပြောင်းလဲနိုင်ပါသည်။

Ruby မှာ **Nokogiri** gem သည် XSLT transformations ကို support လုပ်သည်။

#### **3.1. Using XSLT with Nokogiri**

```ruby
require 'nokogiri'

# Sample XML data
xml_data = <<-XML
<bookstore>
  <book>
    <title>Ruby Programming</title>
    <author>David Flanagan</author>
    <price>39.95</price>
  </book>
</bookstore>
XML

# Sample XSLT stylesheet
xslt_data = <<-XSLT
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <xsl:template match="/">
    <html>
      <body>
        <h1>Books List</h1>
        <table border="1">
          <tr>
            <th>Title</th>
            <th>Author</th>
            <th>Price</th>
          </tr>
          <xsl:for-each select="bookstore/book">
            <tr>
              <td><xsl:value-of select="title"/></td>
              <td><xsl:value-of select="author"/></td>
              <td><xsl:value-of select="price"/></td>
            </tr>
          </xsl:for-each>
        </table>
      </body>
    </html>
  </xsl:template>
</xsl:stylesheet>
XSLT

# Parse XML and XSLT data
xml_doc = Nokogiri::XML(xml_data)
xslt_doc = Nokogiri::XSLT(xslt_data)

# Perform the XSLT transformation
result = xslt_doc.transform(xml_doc)

# Output the result (HTML)
puts result.to_html
```

**Explanation:**
- **`Nokogiri::XSLT(xslt_data)`** သည် XSLT data ကို parse လုပ်ပြီး, **`transform(xml_doc)`** ကို သုံးပြီး XML document ကို transform လုပ်ပါသည်။
- XSLT မှာ XML data ကို HTML format သို့ ပြောင်းပြန်ပြပါသည်။

---

### **4. Validating XML with XSD**

XML data ကို validate လုပ်ရန် **XSD (XML Schema Definition)** ကို အသုံးပြုနိုင်ပါသည်။ Ruby မှာ **Nokogiri** သည် XML data ကို **XSD** schema ဖြင့် validate လုပ်နိုင်ပါသည်။

#### **4.1. Validating XML with XSD Example**

```ruby
require 'nokogiri'

# Sample XML data
xml_data = <<-XML
<bookstore>
  <book>
    <title>Ruby Programming</title>
    <author>David Flanagan</author>
    <price>39.95</price>
  </book>
</bookstore>
XML

# Sample XSD schema
xsd_data = <<-XSD
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <xsd:element name="bookstore">
    <xsd:complexType>
      <xsd:sequence>
        <xsd:element name="book" maxOccurs="unbounded">
          <xsd:complexType>
            <xsd:sequence>
              <xsd:element name="title" type="xsd:string"/>
              <xsd:element name="author" type="xsd:string"/>
              <xsd:element name="price" type="xsd:decimal"/>
            </xsd:sequence>
          </xsd:complexType>
        </xsd:element>
      </xsd:sequence>
    </xsd:complexType>
  </xsd:element>
</xsd:schema>
XSD

# Parse XML and XSD
xml_doc = Nokogiri::XML(xml_data)
xsd_doc = Nokogiri::XML::Schema(xsd_data)

# Validate XML against XSD
if xsd_doc.valid?(xml_doc)
  puts "XML is valid!"
else
  puts "XML is invalid!"
end
```

**Explanation:**
- **`Nokogiri::XML::Schema(xsd_data)`** သည် XSD schema ကို parse လုပ်ပြီး, **`valid?(xml_doc)`** ကို အသုံးပြုပြီး XML data ကို validate လုပ်ပါသည်။
- `valid?` method သည် XML ကို XSD နှင့် တစ်ညီတစ်မျှ ထားမရှိခဲ့ပါက `false` ကို return ပြန်ပါသည်။

---

### **Conclusion**

Ruby မှာ **XML**, **XSLT**, နှင့် **XPath** ကို **Nokogiri** gem သုံးပြီး လွယ်ကူစွာ အလုပ်လုပ်နိုင်ပါတယ်။ XML data များကို parse လုပ်ခြင်း, XPath queries လုပ်ခြင်း, XSLT transformations ပြုလုပ်ခြင်းနှင့် XSD schema ဖြင့် validation လုပ်ခြင်းတို့အတွက် Nokogiri က အလွန်အသုံးဝင်သော tool ဖြစ်ပါတယ်။

- **XML** ကို parsing, manipulating, transforming လုပ်နိုင်ခြင်း
- **XPath** ဖြင့် XML data မှ elements ရှာဖွေရန်
- **XSLT** ဖြင့် XML ကိုအခြား format များသို့ပြောင်းလဲရန်
- **XSD** ဖြင့် XML data ကို validate လုပ်နိုင်ခြင်း

Ruby နှင့် Nokogiri သည် XML-based applications များ ဖော်ဆောင်ရာတွင် အလွန်ထိရောက်ပြီး powerful tool ဖြစ်ပါတယ်။