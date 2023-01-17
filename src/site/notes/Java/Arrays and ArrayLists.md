---
{"dg-publish":true,"permalink":"/java/arrays-and-array-lists/"}
---


# Arrays and ArrayLists

---

01-16-2023

Even though Java arrays and arrayLists are reference types, there is a distinct difference in how we can interact with them. 

An array is a fixed-size data structure that stores a collection of elements of the same data type. An ArrayList, on the other hand, is a dynamic, resizable version of an array. It can also store a collection of elements, but it can grow or shrink as needed.

First you must import the classes to use them:
```java
// Importing required classes
import java.util.ArrayList;
import java.util.Arrays;
```


Here's an example of how to create an array in Java:

```java
int[] myArray = new int[5];

int[] myArray = { 1, 2, 3, 4, 5 }
```

This creates an array that can hold 5 integers, or declare the elements in the array

Here's an example of how to create and add to an ArrayList in Java:

```java
ArrayList<Integer> myArrayList = new ArrayList<Integer>();

        myArrayList.add(1);
        myArrayList.add(2);
        myArrayList.add(3);
        myArrayList.add(4);
```

This creates an empty ArrayList that can hold integers.

To access or modify an element in an array, you can use the array's index, like this:

```java
int firstElement = myArray[0];

myArray[0] = 10;
```

To access or modify an element in an ArrayList, you can use the `get()` method, like this:

```java
int firstElement = myArrayList.get(0);

myArrayList.set(0, 10); // value is primitive but is converted to ref type
myArrayList.set(0, Integer.valueOf(10)); // passed value as reference type
// both are acceptable
```

Here's an example of how to delete an element from an ArrayList in Java:

```java
ArrayList<Integer> myArrayList = new ArrayList<Integer>(Arrays.asList(1, 2, 3, 4, 5));
int indexToRemove = 2;
myArrayList.remove(indexToRemove); // Output: [1, 2, 4, 5]

// alternatively
myArrayList.remove(Integer.valueOf(2)); 

System.out.println(Arrays.toString(myArrayList)); // Output: [1, 4, 5]
```

Note that removing elements from an ArrayList is more efficient than removing elements from an array, because an ArrayList is implemented as a dynamic data structure and it can resize itself automatically.