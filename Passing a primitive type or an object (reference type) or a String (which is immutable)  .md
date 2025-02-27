```java
public class JavaTech {
	
	public void changeValue1(int age) {
		age = 30;
		System.out.print("\n in changeValue1 \n");
		System.out.print(age);
	}
	
	public void changeValue2(Person person) {
		person.setName("newName");
	}
	
	public void changeValue3(String str) {
		
		str = "newStr";
		System.out.print("\n in changeValue3 \n");
		System.out.print(str);
	}

	public static void main(String[] args) {
		
		// TODO Auto-generated method stub
	
		JavaTech javaTech = new JavaTech();
		int age = 20;
		System.out.print(age);
		javaTech.changeValue1(age);
		System.out.print("\n");
		System.out.print(age);

		Person person = new Person("name",10);
		System.out.print("\n");
		System.out.print(person.getName());
		javaTech.changeValue2(person);
		System.out.print("\n");
		System.out.print(person.getName());
		
		String str = "str";
		System.out.print("\n");
		System.out.print(str);
		javaTech.changeValue3(str);
		System.out.print("\n");
		System.out.print(str);
	}
}
```
# 1. Passing a primitive type (int) in changeValue1 method:
```java

public void changeValue1(int age) {
    age = 30;
    System.out.print("\n in changeValue1 \n");
    System.out.print(age);
}
```
Here, you're passing the age variable (which is of type int) to the method. Java passes primitive types by value, which means a copy of the value is passed. Inside the method, age gets changed to 30, but this does not affect the original age in the main method. The printed output will show 30 inside the method, but the original age in main will remain unchanged.

Expected Output:


20
 in changeValue1 
30
20
# 2. Passing an object (reference type) in changeValue2 method:
```java
public void changeValue2(Person person) {
    person.setName("newName");
}
```
Here, you're passing a Person object, which is a reference type, to the method. Java passes reference types by value, meaning it passes the value of the reference (the address) to the method. Inside the method, the setName method changes the state of the object the reference points to. This change will be reflected outside the method, as both the main method and the changeValue2 method are working on the same object.

Expected Output:
name
newName

# 3. Passing a String (which is immutable) in changeValue3 method:
```java

public void changeValue3(String str) {
    str = "newStr";
    System.out.print("\n in changeValue3 \n");
    System.out.print(str);
}
```
Although String is a reference type, it's immutable in Java. This means you cannot modify the original string; any operation on a String creates a new String object. When you change str to "newStr", it points to a new object, but it does not change the original str reference in the main method.

Expected Output:

str
 in changeValue3 
newStr
str

# Key Takeaways:

Primitives (like int) are passed by value, meaning the method gets a copy, and changes do not affect the original variable.

Reference types (like Person or String) are passed by value of the reference, meaning the method can modify the object’s state, but not the reference itself.

String is a special case, as it is immutable, so when you assign a new value to a String, you're actually pointing to a new object, leaving the original string unchanged.
