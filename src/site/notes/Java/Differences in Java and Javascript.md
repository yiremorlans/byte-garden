---
{"dg-publish":true,"permalink":"/java/differences-in-java-and-javascript/"}
---


## Key concept differences in Java and Javascript

---

01-14-2023

One major difference is that Java is a compiled language, while JavaScript is an interpreted language. This means that Java code is compiled into machine code before it is executed, while JavaScript code is interpreted and executed directly by the browser or JavaScript engine.

Another difference is the way they are used. Java is primarily used for building standalone applications, such as desktop and mobile apps, while JavaScript is mainly used for creating interactive elements on websites and web applications.

Here are some code examples to illustrate these differences:
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

In the Java example, the code is defining a class called "HelloWorld" with a main method, which is the entry point for the application. The main method then uses the built-in "System.out.println" method to print "Hello, World!" to the console.

```js
console.log("Hello, World!");
```

In the JavaScript example, the code is using the built-in "console.log" method to print "Hello, World!" to the browser's developer console.

Another key difference is the way they handle Object Oriented Programming. Java follows a class-based OOP model, while JavaScript follows a prototype-based OOP model.

```java
class Dog {
    String breed;
    int age;
    String color;
 
    void barking() {
    }
 
    void hungry() {
    }
 
    void sleeping() {
    }
}

```

In the Java example, the code defines a class called "Dog" with properties (breed, age, color) and methods (barking(), hungry(), sleeping()). A new instance of the class can be created using the 'new' keyword.

```js
let dog = {
  breed: "",
  age: 0,
  color: "",
  barking: function() {},
  hungry: function() {},
  sleeping: function() {}
};

```

In the JavaScript example, the code defines an object called "dog" with properties (breed, age, color) and methods (barking(), hungry(), sleeping()). The object is created by assigning the object literal to a variable.
