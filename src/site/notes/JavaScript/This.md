---
{"dg-publish":true,"permalink":"/java-script/this/"}
---


# JavaScript's `this` keyword in various contexts

---

02-28-2023

## What the heck is `this`?

JavaScript’s `this` keyword is a source of confusion for new and experienced developers alike. It can be frustrating if, for some reason, `this` doesn’t point to the context that was intended.

JavaScript's `this` keyword behaves differently depending on its runtime environment because the global object is different in each environment. In the browser, the global object is 'window', while in Node.js, it is 'global'. Therefore, the `this` keyword will refer to the global object in each environment.

The "use strict" statement influences what the `this` keyword points to. In strict mode, the `this` keyword inside a function will be undefined if the function is called without an explicit `this` context. In non-strict mode, the `this` keyword will refer to the global object if the function is called without an explicit `this` context.

Here are the different ways the `this` keyword behaves in different contexts:

1. Global context: When `this` is used in the global context, it refers to the global object of the runtime environment. 

```javascript
// BROWSER
// "use strict";
console.log(this === window); // true

// NODE REPL
console.log(this === global); // true
```

However, within a node *module* we get **false**. This is because, in the top-level code of a node module, this is equivalent to module.exports, not global.

2. Function calls: When a function is called, the `this` keyword refers to the object that the function is called on, or the global object if the function is called without an explicit `this` context.

```javascript
function greet() {
  console.log(this.name);
}

const person = {
  name: 'Yire',
  greet: greet
};

person.greet(); // Yire

const func = greet;
func(); // undefined in strict mode, Window in non-strict mode
```

3. Constructor calls: When a constructor function is used with the 'new' keyword, `this` refers to the instance of the object that is being created.

```javascript
function Person(name) {
  this.name = name;
}

const yire = new Person('Yire');
console.log(yire.name); // Yire
```

4. Method calls: When a method is called on an object, `this` refers to the object that the method is called on.

```javascript
const person = {
  name: 'Yire',
  greet: function() {
    console.log('Hello, my name is ' + this.name);
  }
};

person.greet(); // Hello, my name is Yire
```

Sometimes, you may want to explicitly set the `this` context for a function call using .call() or .apply(). These methods are used to call a function with a specified `this` context, as well as arguments.

```javascript
function greet() {
  console.log('Hello, my name is ' + this.name);
}

const person = { name: 'Yire' };
greet.call(person); // Hello, my name is Yire
greet.apply(person); // Hello, my name is Yire
```

If you want to permanently set the `this` context for a function, you can use .bind(). This creates a new function with the `this` context set to the specified object.

```javascript
function greet() {
  console.log('Hello, my name is ' + this.name);
}

const person = { name: 'Yire' };
const boundGreet = greet.bind(person);
boundGreet(); // Hello, my name is Yire
```

Arrow functions behave differently with the `this` keyword. They do not have their own `this` context, and instead use the `this` value from their enclosing execution context. They should not be used as methods for objects because then `this` does not work at all.

```javascript
const person = {
  name: 'Yire',
  greet: () => {
    console.log('Hello, my name is ' + this.name);
  }
};

person.greet(); // Hello, my name is undefined
```

In this example, the arrow function is used inside the `forEach()` method to log a message to each friend in the `friends` array. The arrow function captures the `this` value from its enclosing execution context, which is the `person` object. Therefore, when the arrow function is called, it uses the `this` value of `person`, and logs the correct message for each friend, including the name of the person who is greeting them.

![](https://nookipedia.com/wiki/Marshal/Gallery#/media/File:Marshal_NH_Villager_Icon.png)
```javascript
const person = {
  name: 'Yire',
  friends: ['Marshal', 'Raymond', 'Sherb'],
  greetFriends: function() {
    this.friends.forEach(friend => {
      console.log(`Hi ${friend}, I'm ${this.name}`);
    });
  }
};

person.greetFriends();
// Hi Marshal, I'm Yire
// Hi Raymond, I'm Yire
// Hi Sherb, I'm Yire
```