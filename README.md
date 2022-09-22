## Spring REST - Overview , JSON Data Binding

REST: REpresentational State Transfer
+ Lightweight approach for communication between applications
+ Rest is language independent
+ The **client** application can use **ANY** programming language
+ The **server** application can use **ANY** programming language


**What is the data format?**
+ REST application can use any data format
+ Commonly see XML and JSON
+ JSON is most popular and modern
    + JavaScript Object Notation

**What is JSON?**

+ JavaScript Object Notation
+ Lightweight data format for storing and exchanging data ... plain text
+ Language independent ... not just for **JavaScript**
+ Can use with any programming language: **Java, C#, Python** etc ...

> JSON is just plain text data

**Simple JSON Example**

+ Curley braces define objects in JSON
+ Object members are name / value pairs
    + Delimited by colons

+ Name is **always** in double-quotes

```JSON
{
  "id": 14,
  "firstName": "Mario",
  "lastName": "Rossi",
  "active": true
  "course": null
}
```
+ `"id"` in Name
+ `14` is Value

**JSON Values**

+ Number: no quotes
+ String: in double quotes
+ Boolean: **true, false**
+ Nested JSON object
+ Array
+ **null**

**Nested JSON Objects**

```JSON
{
  "id": 14,
  "firstName": "Mario",
  "lastName": "Rossi",
  "active": true
  "address": {
              "street": "Tibi str 6",
              "city": "Duisburg",
              "postalCode": 47051,
              "country": "DE"
            }
}
```


**JSON Arrays**

```JSON
{
  "id": 14,
  "firstName": "Mario",
  "lastName": "Rossi",
  "languages": ["java", "C#", "Python", "Javascript"]
}
```
+ Arrays use square brackets [...]

**Java JSON Data Binding**

+ Data binding is the process of converting JSON data to a Java POJO

<img src="https://user-images.githubusercontent.com/80107049/191795985-841aa2f6-3cc0-4c3f-945c-be0bb1edecc8.png" width="500" />



> Also known as, Mapping , Serialization/Deserialization, Marshalling/Unmarshalling

**JSON Data Binding with Jackson**

+ Spring uses the **Jackson Project** behind the scenes
+ Jackson handles data binding between JSON and Java POJO
+ Details on Jackson Project: https://github.com/FasterXML/jackson
+ Jackson supports XML and JSON
+ Jackson Data Binding API
    + Package:**come.fasterxml.jackson.databind**

+ Maven Dependency

```XML
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>2.9.0</version>
</dependency>
```
+ By default, Jackson will call appropriate getter/setter method

**JSON to Java POJO**

```JAVA
import java.io.File;
import com.fasterxml.jackson.databind.ObjectMapper;

public class Driver {
  
  public static void main(String[] args) throws Exception {
    
    // create object mapper
    ObjectMapper mapper = new ObjectMapper();
    
    // read JSON from file and map/convert to Java POJO
    Student myStudent = mapper.readValue(new File("data/sample.json"), Student.class);
    
    // also print individual items
    System.out.println("First name = " + myStudent.getFirstName());
    System.out.Println("Last name = " + myStudnet.getLastName());
   
  }
}   
```

+ `"data/sample.json"` Rad data from this file
+ `Student.class` Create an instance of this class and populate it









**Java POJO to JSON**
```JAVA
// create object mapper
ObjectMapper mapper = new ObjectMapper();

// read JSON file and map/convert to Java POJO
Student myStudent = mapper.readValue(new File("data/sample.json"), Student.class);

...
  
// now write JSON to output file
mapper.enable(SerializationFeature.INDENT_OUTPUT);
mapper.writerValue(now File("data/outout.json"), myStudent);
```
+ Jackson calls the getter methods on Student POJO to create JSON output file


**Spring and Jackson Support**

+ When building Spring REST applications
+ Spring will automatically handle Jackson Integration
+ JSON data being passed to REST controller is converted to POJO
+ Java object being returned from REST controller is converted to JSON




