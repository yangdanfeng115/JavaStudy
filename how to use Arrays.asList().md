# The issue with your code lies in the fact that Arrays.asList() returns a fixed-size list, meaning you cannot modify its size by adding or removing elements.

```java

List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
list.add(6); // This line will throw an UnsupportedOperationException
```
Arrays.asList() creates a list that is backed by the original array. The size of this list is fixed because it is directly tied to the array’s size.
Calling list.add(6) will throw an UnsupportedOperationException because the list created by Arrays.asList() does not support adding or removing elements.

# How to fix it
If you want to be able to add elements to the list, you can wrap the list in an ArrayList, which is resizeable. Here’s how you can modify your code:

```java

List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
list.add(6); // Now you can add elements
```
Now the list is an ArrayList (which is mutable and can grow or shrink in size), so you can add or remove elements without issues.
