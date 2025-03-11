The **Adapter Design Pattern** is a structural pattern that allows objects with incompatible interfaces to work together by converting the interface of a class into one that a client expects. It acts as a bridge between two incompatible interfaces, allowing them to interact seamlessly.

### Key Concepts:
- **Client**: The class that interacts with the target interface.
- **Target**: The interface that the client expects.
- **Adaptee**: The class or component with an existing interface that is incompatible with what the client expects.
- **Adapter**: A wrapper class that implements the target interface and translates requests from the client into a format the adaptee understands.

### Purpose:
The main purpose of the Adapter pattern is to **reuse existing code** or libraries without modifying them when their interface is different from what your system expects.

### Types of Adapters:
1. **Class Adapter**: Uses inheritance to adapt the interface of one class to another.
2. **Object Adapter**: Uses composition, where the adapter contains an instance of the adaptee and delegates calls to it.

### Example:
Imagine you have a system that expects data from a legacy service that provides XML responses, but you want to use a new service that returns JSON. To avoid rewriting the client code, you can create an adapter that converts the JSON response from the new service into the XML format expected by the client.

```java
// Target interface that the client expects
public interface XMLParser {
    String parseXML();
}

// Adaptee class with a different interface
public class JSONParser {
    public String parseJSON() {
        return "{\"message\": \"Hello JSON\"}";
    }
}

// Adapter class to convert JSON to XML format
public class JSONToXMLAdapter implements XMLParser {
    private JSONParser jsonParser;

    public JSONToXMLAdapter(JSONParser jsonParser) {
        this.jsonParser = jsonParser;
    }

    @Override
    public String parseXML() {
        String json = jsonParser.parseJSON();
        // Convert JSON to XML (mock conversion)
        return "<message>Hello XML</message>";
    }
}

// Client class
public class Client {
    public static void main(String[] args) {
        XMLParser xmlParser = new JSONToXMLAdapter(new JSONParser());
        System.out.println(xmlParser.parseXML());  // Output: <message>Hello XML</message>
    }
}
```

### Benefits:
- **Reusability**: Allows you to use existing code or libraries without altering them.
- **Flexibility**: Decouples the client from the adaptee, promoting flexibility.
- **Interoperability**: Enables the integration of different systems with incompatible interfaces.

### Use Cases:
- When you want to use an existing class, but its interface is not compatible with the system you're working on.
- When you want to create reusable code that works with future or legacy components.

