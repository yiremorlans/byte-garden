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
```

This creates an array that can hold 5 integers.

Here's an example of how to create an ArrayList in Java:

```java
ArrayList<Integer> myArrayList = new ArrayList<Integer>();
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

myArrayList.set(0, Integer.valueOf(10));
```