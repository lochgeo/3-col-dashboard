In Java, `==` and `equals()` are used to compare objects, but they serve different purposes and operate in different ways.

### `==` Operator
The `==` operator is used to compare the references of two objects to check if they point to the same memory location. It is a reference comparison, not a value comparison.

- **Primitive Types:** When used with primitive types (e.g., `int`, `char`), `==` compares the actual values.
  ```java
  int a = 5;
  int b = 5;
  System.out.println(a == b); // true
  ```
- **Object References:** When used with object references, `==` checks if both references point to the same object in memory.
  ```java
  String s1 = new String("hello");
  String s2 = new String("hello");
  System.out.println(s1 == s2); // false
  String s3 = s1;
  System.out.println(s1 == s3); // true
  ```

### `equals()` Method
The `equals()` method is intended to compare the values of two objects for equality. This method is defined in the `Object` class and can be overridden by user-defined classes to provide value-based equality.

- **Default Implementation:** The default implementation of `equals()` in the `Object` class compares object references (similar to `==`).
  ```java
  Object obj1 = new Object();
  Object obj2 = new Object();
  System.out.println(obj1.equals(obj2)); // false
  System.out.println(obj1.equals(obj1)); // true
  ```
- **Overridden Implementation:** Many classes, such as `String`, `Integer`, etc., override the `equals()` method to compare values.
  ```java
  String str1 = new String("hello");
  String str2 = new String("hello");
  System.out.println(str1.equals(str2)); // true

  Integer num1 = new Integer(100);
  Integer num2 = new Integer(100);
  System.out.println(num1.equals(num2)); // true
  ```

### Key Differences
1. **Purpose:**
   - `==` is used for reference comparison (i.e., checking if two references point to the same object).
   - `equals()` is used for value comparison (i.e., checking if two objects are logically "equal").

2. **Primitives vs. Objects:**
   - `==` works for both primitives and object references.
   - `equals()` works only for objects and must be overridden to perform a meaningful value comparison.

3. **Default Behavior:**
   - The default behavior of `==` cannot be changed.
   - The behavior of `equals()` can be overridden in a class to define what it means for two instances to be equal.

### Practical Example
Consider a custom class `Person`:
```java
class Person {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Overriding equals() to compare values of name and age
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Person person = (Person) obj;
        return age == person.age && name.equals(person.name);
    }
}

public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("John", 30);
        Person p2 = new Person("John", 30);
        Person p3 = p1;
        
        System.out.println(p1 == p2); // false, different references
        System.out.println(p1.equals(p2)); // true, same name and age
        System.out.println(p1 == p3); // true, same reference
    }
}
```
In this example:
- `p1 == p2` is `false` because `p1` and `p2` are different objects.
- `p1.equals(p2)` is `true` because the `equals()` method is overridden to compare the `name` and `age` values.
- `p1 == p3` is `true` because `p3` references the same object as `p1`.
