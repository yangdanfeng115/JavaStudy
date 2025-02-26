```java
public class JavaTech {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
	
	Integer a = Integer.valueOf(100);
	Integer b = Integer.valueOf(100);
	System.out.println(a == b);
	System.out.println(a.equals(b));
	
	
	Integer a1 = Integer.valueOf(900);
	Integer b1 = Integer.valueOf(900);
	int c1 = 900;
	System.out.println(a1 == b1);
	System.out.println(a1.equals(b1));
	System.out.println(a1 == c1);

	
	}

}
```

Key Concepts in the Code:
# Autoboxing:
Java automatically converts primitive data types (like int) into their wrapper classes (like Integer) when needed. This process is called autoboxing.
Integer Caching:
The Integer class in Java caches values between -128 and 127 by default. This means when you call Integer.valueOf(100) or any other number within that range, it returns the same object rather than creating a new one each time.
# Unboxing:
Java can also automatically convert wrapper objects back into primitive types when necessary. This process is called unboxing.
# Analysis of the Code
## 1. The first block:
```java

Integer a = Integer.valueOf(100);
Integer b = Integer.valueOf(100);
System.out.println(a == b);
System.out.println(a.equals(b));
```
Integer.valueOf(100):
The value 100 is within the cached range (-128 to 127), so Java will reuse the cached object for both a and b. This means a and b point to the same object in memory.

a == b:
The == operator compares object references (memory addresses), not the actual values. Since both a and b refer to the same object in memory (due to caching), the comparison will return true.

a.equals(b):
The .equals() method in the Integer class compares the values of the two Integer objects. Since both a and b have the value 100, the comparison will return true.
Output for this block:

true
true
## 2. The second block:
```java

Integer a1 = Integer.valueOf(900);
Integer b1 = Integer.valueOf(900);
int c1 = 900;
System.out.println(a1 == b1);
System.out.println(a1.equals(b1));
System.out.println(a1 == c1);
```
Integer.valueOf(900):

The value 900 is outside the cached range (-128 to 127), so Java will create a new object each time Integer.valueOf(900) is called. This means a1 and b1 will not refer to the same object, even though their values are the same.

a1 == b1:

The == operator compares object references. Since a1 and b1 are two different objects (even though both have the value 900), the result will be false.

a1.equals(b1):

The .equals() method compares the values of the two Integer objects. Since both a1 and b1 have the value 900, the result will be true.

a1 == c1:

a1 is an Integer object, and c1 is a primitive int. The == operator will trigger unboxing to convert a1 to an int, and then compare the values. Since a1 contains the value 900, and c1 is also 900, the comparison will return true.
Output for this block:

false
true
true

# Summary of the Results:
## First block (a == b, a.equals(b)):
a == b: 
true (Because a and b refer to the same object in memory, thanks to the cache for values between -128 and 127).

a.equals(b):
true (Because the values of a and b are equal).

## Second block (a1 == b1, a1.equals(b1), a1 == c1):
a1 == b1: 
false (Because a1 and b1 are different objects, even though their values are the same, due to the lack of caching for values outside the range -128 to 127).
a1.equals(b1): 
true (Because the values of a1 and b1 are equal).
a1 == c1: 
true (Because a1 is unboxed to an int and compared with the primitive value c1, which is also 900).
## Key Points:
### Integer Caching: 
Java caches Integer values between -128 and 127. For values within this range, Integer.valueOf() will return the same object, which explains why a == b returns true for 100. For values outside this range (like 900), new Integer objects are created, so a1 == b1 returns false.

### Autoboxing and Unboxing:

Autoboxing occurs when you assign an int to an Integer (like int c1 = 900;), and unboxing happens when you compare an Integer with an int (like a1 == c1). In this case, unboxing converts a1 to an int before comparing the values.

### == vs. .equals():

== checks reference equality (whether the two references point to the same object).
.equals() checks value equality (whether the two objects have the same value).
