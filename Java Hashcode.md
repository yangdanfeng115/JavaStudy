In Java, the hashCode() method is used to generate an integer value that represents the hash code of an object. It is an important part of the Object class, and it plays a key role in the proper functioning of hash-based collections like HashMap, HashSet, and Hashtable.

# Key Points:

## Default Implementation: 
The hashCode() method in the Object class provides a default implementation that typically generates a unique integer based on the memory address of the object. However, for most custom objects, you'll want to override this method to return a meaningful hash code based on the object's state.

## Contract of hashCode():

### Consistency: 
The hash code of an object must remain consistent during the object's lifetime. If an object’s state does not change, its hash code should not change.
### Equal Objects Have Equal Hash Codes: 
If two objects are considered equal according to the equals() method, they must return the same hash code.
### Unequal Objects: 
If two objects are not equal, their hash codes don't have to be distinct, but it’s good practice to ensure they are.

## Example: Overriding hashCode()

When you override the equals() method for a custom object, you should also override hashCode() to ensure proper behavior in hash-based collections.

Here's an example of how to override both equals() and hashCode():

```java

import java.util.Objects;

public class Person {
    private String name;
    private int age;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Person person = (Person) obj;
        return age == person.age && name.equals(person.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);  // A clean and reliable way to generate hash code
    }

    // Getter methods for name and age
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```
## Explanation:
### equals(): 
We override this method to compare name and age because two Person objects with the same name and age should be considered equal.
### hashCode(): 
The Objects.hash() method generates a hash code based on the fields we want to include in the equality check. It’s a convenient and reliable way to ensure a good distribution of hash codes.
### Why Overriding hashCode() is Important:
When you put objects into a collection like HashMap, the hash code determines where the object will be placed in the underlying hash table. If two objects are equal but have different hash codes, it can cause logical errors because the HashMap might not be able to find the object even though it is logically equal to another one.
