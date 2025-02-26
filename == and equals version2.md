```
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
public class JavaTech {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
	
		String s1 = new String("abc");
		String s2 = new String("abc");
		System.out.println(s1 == s2);
		System.out.println("\n");

		System.out.print(s1.equals(s2));
		System.out.println("\n");

		Set<String> set1 = new HashSet<>();
		set1.add(s1);
		set1.add(s2);
		
		System.out.println(set1.size());
		
		System.out.println("\n");

	    System.out.println(s1.hashCode());

		System.out.println("\n");

	    System.out.println(s2.hashCode());
	    
		System.out.println("\n");


		Person p1 = new Person("abc",10);
		Person p2 = new Person("abc",10);
		System.out.println(p1 == p2);
		
		System.out.println("\n");

		System.out.print(p1.equals(p2));
		
		System.out.println("\n");

		Set<Person> set2 = new HashSet<>();
		set2.add(p1);
		set2.add(p2);
		
		System.out.println(set2.size());
		
		System.out.println("\n");

	    System.out.println(p1.hashCode());

		System.out.println("\n");

	    System.out.println(p2.hashCode());
	    
		System.out.println("\n");

	
	}

}
```
Let's walk through the code and analyze the output step by step, considering the Person class has overridden the equals() and hashCode() methods.

Code Explanation:
# 1. String comparison (s1 and s2):
```java

String s1 = new String("abc");
String s2 = new String("abc");
System.out.println(s1 == s2);  // Compare references
System.out.print(s1.equals(s2));  // Compare values
```
## s1 == s2: 

The == operator checks for reference equality. Since s1 and s2 are created using new keyword, they refer to two different objects in memory. Hence, s1 == s2 will be false.

## s1.equals(s2): 

The .equals() method in the String class compares the values of the strings. Since both s1 and s2 contain the same string "abc", s1.equals(s2) will be true.

## Output:


false
true
# 2. Adding String objects to a HashSet:
```java

Set<String> set1 = new HashSet<>();
set1.add(s1);
set1.add(s2);
System.out.println(set1.size());
```

A HashSet removes duplicates based on the hashCode() and equals() methods.
Since the String class already overrides hashCode() and equals(), and both s1 and s2 have the same value "abc", they will be treated as equal objects and only one element will be added to the set.
## Output:

1

# 3. Printing hashCode of s1 and s2:
```java

System.out.println(s1.hashCode());
System.out.println(s2.hashCode());
```
The hashCode() of both s1 and s2 will be the same because they have the same value "abc". The hashCode() for a string is computed based on the string content.
## Output (hash code will be the same for both, but the exact value depends on the implementation):


96354
96354
# 4. Comparison of Person objects (p1 and p2):
```java

Person p1 = new Person("abc", 10);
Person p2 = new Person("abc", 10);
System.out.println(p1 == p2);  // Compare references
System.out.print(p1.equals(p2));  // Compare values (overridden equals)
```
## p1 == p2:
The == operator checks for reference equality. Since p1 and p2 are created using the new keyword, they are two different objects with different memory addresses. Therefore, p1 == p2 will be false.

## p1.equals(p2): 
The Person class overrides the .equals() method to compare the values of name and age. Since both p1 and p2 have the same name "abc" and age 10, p1.equals(p2) will be true.

## Output:

false
true
# 5. Adding Person objects to a HashSet:

```java

Set<Person> set2 = new HashSet<>();
set2.add(p1);
set2.add(p2);
System.out.println(set2.size());
```
A HashSet removes duplicates based on the hashCode() and equals() methods.
Since Person has overridden both hashCode() and equals(), and p1.equals(p2) is true, only one Person object (either p1 or p2) will be added to the set2. So, the size of the set will be 1.

## Output:

1

# 6. Printing the hashCode of p1 and p2:
``` java

System.out.println(p1.hashCode());
System.out.println(p2.hashCode());
```
Since Person has overridden hashCode() using the Objects.hash(name, age) method, both p1 and p2 will have the same hash code, because they have the same name and age values.
## Output (hash codes will be the same, but the exact value depends on the name and age):


9622
9622

# Final Output Summary:

false
true

1

96354
96354

false
true

1

9622
9622

# Key Points:

## String Comparison:

== compares references.
.equals() compares values for strings.
In HashSet, duplicate strings are removed based on equals() and hashCode().

## Person Comparison:

== compares references (memory addresses).
.equals() compares values (overridden in Person to compare name and age).
In HashSet, Person objects are treated as duplicates if their equals() and hashCode() methods return equivalent results.

## HashSet and hashCode()/equals():

A HashSet uses both hashCode() and equals() to determine if two objects are duplicates. If both methods indicate that two objects are equal, only one will be stored in the set.
