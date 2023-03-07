---
{"dg-publish":true,"permalink":"/ds-and-algorithms/linked-lists/"}
---


# Differences Between Linked Lists & Arrays

---

03-07-2023


A linked list and an array are both data structures used in programming, but they have some important differences in the way they store and access data.

An array is a collection of elements of that are stored in a contiguous block of memory. This means that all the elements are stored one after another, and you can access them using an index. Arrays are good for storing and accessing data quickly and efficiently, especially when you know the size of the array beforehand.

```javascript
// javascript arrays may hold Number, String, Boolean, even Object data types
let arr = [1, 2, '3', true, null];
console.log(arr[1]); // 2

arr.push(6); 
arr.shift(); // 1
console.log(arr); // [2, '3', true, null, 6];

arr.unshift('Dog');
console.log(arr); // ['Dog', 2, '3', true, null, 6]
```

### Time/Space Complexity
---

A linked list, on the other hand, is a collection of elements that are linked together using pointers. Each element in the list contains a value and a pointer to the next element in the list. Because the elements are not stored in a contiguous block of memory, linked lists can be more flexible than arrays, and they can grow or shrink dynamically. However, accessing an element in a linked list can be slower than in an array because you have to follow the pointers to find the element.