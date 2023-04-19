---
{"dg-publish":true,"permalink":"/java-script/promise-object/"}
---


# Handling `Promise` objects in various contexts

---

## What is a `Promise` in JavaScript?

04-18-2023

A `Promise` is an object that represents a value that might not be available yet, but will be at some point in the future. A `Promise` can be in one of three states: "pending" (the initial state, before the `Promise` has resolved or been rejected), "fulfilled" (meaning the operation completed successfully and returned a value), or "rejected" (meaning the operation failed and returned an error).

```javascript
async function fetchData() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
    if (response.ok) {
      const data = await response.json();
      return data;
    } else {
      throw new Error('Error fetching data');
    }
  } catch (error) {
    throw new Error(error.message);
  }
}
```

In this example, we're defining an async function called `fetchData` that makes an HTTP request using `fetch` and returns a `Promise` that resolves with the response data if the request is successful, or rejects with an error if the request fails.

Using async/await syntax allows us to write the same functionality in a more concise and readable way, without having to chain multiple `.then()` calls. We can also handle errors using try/catch blocks, which makes the code more organized and easier to maintain.

Here are built-in JavaScript methods to handle promises in different contexts:

1. **`Promise.all()`** waits for all fulfillments (or the first rejection): 

```javascript
async function fetchData() {
  const [result1, result2] = await Promise.all([
    fetch('https://api.example.com/data1'),
    fetch('https://api.example.com/data2')
  ]);

  const data1 = await result1.json();
  const data2 = await result2.json();

  console.log('Data 1:', data1);
  console.log('Data 2:', data2);
}

fetchData();
```

Use `Promise.all()` to resolve multiple promises when there are multiple related asynchronous tasks that the overall code relies on to work successfully — all of whom we want to fulfill before the code execution continues. It will reject immediately upon **any** of the input promises rejecting.

2. **`Promise.any()`** static method takes an iterable of promises as input and returns a **single** `Promise`:

```javascript
async function fetchData() {
  const result = await Promise.any([
    fetch('https://api.example.com/data1'),
    fetch('https://api.example.com/data2')
  ]);

  const data = await result.json();

  console.log('Data:', data);
}

fetchData();
```

Here we're using `Promise.any()` to resolve the first HTTP request that doesn't reject, and then using `await` to parse the response data using `.json()`, and log the data to the console. It will only reject if all the promises in the array are rejected.


3. **`Promise.race()`** static method also takes an iterable (array) of promises and returns a single `Promise`:

```javascript
async function fetchData() {
  const result = await Promise.race([
    fetch('https://api.example.com/data1'),
    fetch('https://api.example.com/data2')
  ]);

  const data = await result.json();

  console.log('Data:', data);
}

fetchData();
```

`Promise.race()` will return the first `Promise` that either resolves or rejects, whichever comes first. This means that if the first `Promise` to settle is a rejection, the returned `Promise` will reject with the same rejection reason, even if other promises in the array later resolve.

### When to use `Promise.race()` over `Promise.any()`

`Promise.any()` and `Promise.race()` are both Promise methods that return the first resolved Promise from an array of Promises. However, there is a subtle difference in their behavior that determines when to use one over the other.

So, if you want to get the first resolved Promise from an array of promises, and you're only interested in resolving promises, you should use `Promise.any()`. If you want to get the first settled `Promise`, regardless of whether it resolves or rejects, you should use `Promise.race()`.

For example, if you're making multiple HTTP requests and only care about the response from the first successful request, you would use `Promise.any()`. However, if you need to handle errors and want to stop further processing when the first error occurs, you would use `Promise.race()`.

### `Promise` object built-in methods

In addition to `Promise.all()`, `Promise.race()`, and `Promise.any()`, there are several other built-in methods for handling promises in JavaScript.

-   `Promise.allSettled()`: This method returns a `Promise` that resolves when all the promises in an array have settled, meaning they have either resolved or rejected. The returned `Promise` resolves with an array of objects representing the fulfillment value or rejection reason of each `Promise`.
    
-   `Promise.resolve()`: This method returns a `Promise` that is resolved with the given value. This is useful when you want to convert a non-Promise value into a `Promise`.
    
-   `Promise.reject()`: This method returns a `Promise` that is rejected with the given reason. This is useful when you want to create a rejected `Promise` with a specific reason.
    
-   `Promise.prototype.catch()`: This method is used to handle errors that occur in a `Promise` chain. It registers a callback to be called if the Promise is rejected, and returns a new `Promise` that resolves with the return value of the callback.
    
-   `Promise.prototype.finally()`: This method is used to perform an action regardless of whether the `Promise` is resolved or rejected. It registers a callback to be called when the Promise is settled, and returns a new `Promise` that resolves with the original promise's value or rejection reason.

I encourage you to check out the [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) for these methods to learn more about their use cases and see examples of how they can be used in practice.