---
{"dg-publish":true,"permalink":"/interview-prep/anatomy-of-a-java-class/"}
---

# Java anatomy of a class, access modifiers, and keywords

---

{{date}}
```java
public class Main { 
// Static method 
	static void myStaticMethod() { 
	System.out.println("Static methods can be called without creating objects"); } 
	// Public method 
	public void myPublicMethod() { 
	System.out.println("Public methods must be called by creating objects"); 
	} 
	
	// Main method 
	public static void main(String[ ] args) { 
	myStaticMethod(); // Call the static method 
	myPublicMethod(); //This would output an error 
	
	Main myObj = new Main(); // Create an object of Main 
	myObj.myPublicMethod(); // Call the public method 
		} 
	}
```

This code defines a Java class called "Main" with three methods: "myStaticMethod", "myPublicMethod", and "main".

-   The "myStaticMethod" method is defined as static, which means it can be called without creating an object of the "Main" class. This is demonstrated in the "main" method, where "myStaticMethod()" is called directly.

-   The "myPublicMethod" method is defined as public, which means it can be called by any other class or object. However, since it is not static, it must be called on an object of the "Main" class. This is demonstrated in the "main" method, where a new object of "Main" is created with "Main myObj = new Main();" and the method is called on that object with "myObj.myPublicMethod();".

-   The "main" method is the entry point of the program, where the program starts executing, it calls the static method myStaticMethod() which prints "Static methods can be called without creating objects" and creates an object of Main class and call the public method myPublicMethod() which prints "Public methods must be called by creating objects"

## Acess Modifiers

In Java, access modifiers are keywords used to set the level of access to a class, method, or variable. There are four main access modifiers in Java:

1.  `public`: A class, method, or variable that is public can be accessed by any other class, regardless of where it is located in the program.
    
2.  `private`: A class, method, or variable that is private can only be accessed within the same class in which it is defined.
    
3.  `protected`: A class, method, or variable that is protected can be accessed within the same package, or by a subclass in a different package.
    
4.  `default` (also called package-private): A class, method, or variable that does not have any access modifier specified is by default package-private and can only be accessed within the same package.
    

It's important to note that generally speaking, it's better to use the most restrictive access level that still allows the code to function properly. This makes it more difficult for bugs to be introduced, and makes the code more robust and maintainable.