---
{"dg-publish":true,"permalink":"/ds-and-algorithms/linked-lists/"}
---


# Differences Between Linked Lists & Arrays

---

03-07-2023

A linked list and an array are both data structures used in programming, but they have some important differences in the way they store and access data.

## Arrays 

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

// O(n) linear searching method
console.log(arr.indexOf('3')) // 2
```
<br>

### Time/Space Complexity

---

- Generally, accessing an element by index in an array is a constant-time operation with a time complexity of O(1), because the index can be used to calculate the memory address of the element directly. 
- `push()` - O(1), assuming there is available space in the array. However, if the array needs to be resized because there is not enough memory, the time complexity could be O(n), where n is the number of elements in the array before resizing.
- `indexOf()` - requires a linear search, which can have a time complexity of O(n) in the worst case, where n is the number of elements in the array.
- `unshift()` - O(n), all the elements in the array need to be moved to make room for the new element. 
- `shift()` - O(n), the entire array needs to shift one over to occupy the now empty space in memory. 

 Additionally, if there is not enough free space at the beginning of the array to accommodate the new element, the entire array may need to be relocated to a different spot in memory. This can have a space complexity of O(n), where n is the number of elements in the array, because a new block of memory must be allocated and the existing elements must be copied over to the new location.

---

## Linked List

A linked list is a collection of elements that are linked together using pointers. Each element in the list contains a value and a reference to the location of the next element in the list. Because the elements are not stored in a contiguous block of memory, linked lists can be more flexible than arrays, and they can grow or shrink dynamically. However, accessing an element in a linked list can be slower than in an array because you have to follow the pointers to find the element.

```javascript
// DOUBLY LINKED LIST
class LinkedList {
  constructor () {
    this.head = this.tail = null
  }
  // add to the end of the list / tail
  append(value) {
    // if list is empty
    if (!this.tail) {
      this.head = this.tail = new Node(value)
    }
    // if linkedlist has >= one node
    else {
      let oldTail = this.tail
      this.tail = new Node(value)
      oldTail.next = this.tail
      this.tail.prev = oldTail
    }
  }
  //add to beginning of list / head
  prepend(value) {
    // if list is empty
    if (!this.head) {
      this.head = this.tail = new Node(value)
    }
    // if linkedlist has >= one node
    else {
      let oldHead = this.head
      this.head = new Node(value)
      oldHead.prev = this.head
      this.head.next = oldHead
    }
  }

  deleteHead() {
    // if list is empty (no head)
    if (!this.head) {
      return null
    }
    // if linkedlist has >= 1 node
    else {
      let removedHead = this.head
      // if list has only 1 node left
      if (this.head === this.tail) {
        this.head = this.tail = null
      }
      //if list has >1 node
      else {
        this.head = this.head.next
        this.head.prev = null
      }
      return removedHead.value
    }
  }

  deleteTail() {
    // if list is empty (no tail)
    if (!this.tail) {
      return null
    }
    // if linkedlist has >= one node
    else {
      let removedTail = this.tail
      // if list has only 1 node left
      if (this.head === this.tail) {
        this.tail = this.head = null
      }
      //if list has >1 node
      else {
        this.tail = this.tail.prev
        this.tail.next = null
      }
      return removedTail.value
    }
  }

  search(value) {
    let currentNode = this.head

    while (currentNode) {
      if (currentNode.value === value) {
        return currentNode
      }
      currentNode = currentNode.next
    }

    return null
  }
}

class Node {
  constructor (value, prev, next) {
    this.value = value
    this.next = next || null
    this.prev = prev || null
  }
}
```

In this implementation, the Linked List class has an append method for adding a new element to the tail(end of the list), a prepend method for adding a new element to the head(start of the list), deleting the head and tail nodes, and searching for a specific value in the list. 

Each element in the list is represented by a Node object, which has a value property to store the value of the element, a next property to point to the next element in the list, and a prev property that points to previous element. The head and tail properties of the Linked List class are used to keep track of the first and last elements in the list, respectively.


### Time/Space Complexity

---

The space complexity of a doubly linked list is O(n), where n is the number of nodes in the list. This is because each node in the list requires a constant amount of space to store the node's value and pointers to both the previous and next nodes. The amount of space required for the list grows linearly with the number of nodes in the list. 

>Compared to a singly linked list, a doubly linked list requires more space due to the additional pointer to the previous node in each node, but the additional pointer to the previous node makes it possible to perform certain operations in constant time that would require linear time in a singly linked list.

- The `append`, `prepend`, `deleteHead`, and `deleteTail` methods all have a time complexity of O(1) because they only involve updating pointers to the head or tail nodes, which takes constant time regardless of the size of the list.

- `search(value)` - O(n) - worst case scenario, it needs to traverse the entire list to find the value, which would take linear time proportional to the size of the list.


<br>

Choosing between a linked list and an array depends on the specific requirements of your program and the characteristics of the data you need to store and manipulate. Here are some general guidelines to consider:

-   Use an array if you need constant-time access to elements by index and if the size of the data is fixed or predictable. Arrays are also generally faster and more memory-efficient for iterating over all the elements in the array.
    
-   Use a linked list if you need to insert or delete elements frequently, especially at the beginning or end of the list, or if the size of the data is unpredictable or can grow dynamically. Linked lists are also more memory-efficient for storing sparse data (i.e., data with many empty or null elements) or for situations where the size of the data may exceed the available memory.
    
-   If you need a combination of random access and frequent insertions/deletions, you may want to consider using a hybrid data structure, such as a hash table or a tree.
    

In general, the choice between an array and a linked list involves trade-offs between performance, memory usage, and ease of implementation. It's important to carefully analyze the specific requirements and constraints of your program and to benchmark and test different data structures to determine the optimal choice for your use case.