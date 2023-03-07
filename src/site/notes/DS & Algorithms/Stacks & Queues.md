---
{"dg-publish":true,"permalink":"/ds-and-algorithms/stacks-and-queues/"}
---


# JavaScript Implementations of Data Structures

----

03-02-2023

A stack and a [queue](#Queues) are two data structures used to store and organize data in computer programs. They  are widely used in computer science and programming, and they have many real-life applications you might already be familiar with! 

They are used in browsers for storing the history of visited web pages, in text editors for undo/redo functionality, and in operating systems for managing memory. Queues, on the other hand, are used in many everyday applications, such as ordering food at a restaurant or boarding a plane, where the first person in line is served first. They are also used in computer networks for packet routing, in printers for job scheduling, and in music streaming services for managing song queues.

## Stacks

Imagine a stack is like a pile of plates in a cafeteria. You add new plates to the top of the pile, and when you need to remove a plate, you take the top one off first. This is known as LIFO (Last In, First Out) - the last plate added to the pile is the first one that can be removed.

This is a class in JavaScript that implements a stack data structure using an object for storage. The methods use the `storage` object and the `size` property to keep track of the elements in the stack.

```javascript
class Stack {
	// Constructor function that initializes an empty object storage and sets size to 0
	constructor(){
		this.storage = {}
		this.size = 0
	}

	// Method that adds an element to the top of the stack
	push(element){
		// Increment size and add element to storage at new size index
		this.size++
		this.storage[this.size] = element
		console.log(`Added ${element} to storage!`)
	}

	// Method that removes the top element from the stack
	pop(){
		// Retrieve element from storage using current size index, delete it, and decrement size
		let removed = this.storage[this.size]
		delete this.storage[this.size]
		this.size--
		console.log(`Removed ${removed} from storage!`)
		return removed	
	}

	// Method that returns the top element of the stack
	peek(){
		console.log(`${this.storage[this.size]} is on top of the stack!`)
		return this.storage[this.size]
	}

	// Method that searches for an element in the stack
	search(element){
		// Loop through storage object to find first occurrence of element, log message indicating whether element is found or not, and return element if found
		for (let item in this.storage) {
			if (this.storage[item] === element) {
				console.log(`${element} exists in the storage!`)
				return this.storage[item]
			}
		}
		console.log(`${element} does not exist in the storage!`)
	}

	// Method that checks if the stack is empty
	isEmpty(){
		console.log(this.size === 0)
		return this.size === 0
	}
} 
```

> Note that this implementation does not include a check for an empty or full stack. A stack can overflow if too many elements are pushed onto it, and the stack's storage capacity is exceeded. This can happen in implementations where the stack's storage is a fixed-size array or a pre-allocated memory block. 

### Time/Space Complexity

---

The big O notation for the stack implementation provided in the code is:

-   `push`: O(1) - adding an element to the top of the stack takes a constant amount of time, regardless of the size of the stack.
-   `pop`: O(1) - removing an element from the top of the stack takes a constant amount of time, regardless of the size of the stack.
-   `peek`: O(1) - accessing the top element of the stack takes a constant amount of time, regardless of the size of the stack.
-   `search`: O(n) - searching for an element in the stack requires iterating over all elements in the stack, which takes linear time proportional to the size of the stack.
-   `isEmpty`: O(1) - checking if the stack is empty takes a constant amount of time, regardless of the size of the stack.

Therefore, the overall time complexity of the stack implementation is O(n) for the worst-case scenario, which occurs when searching for an element in the stack. However, in the average case, the time complexity is O(1) for all operations except for search.

The space complexity implementation provided is O(n), where n is the number of elements stored in the stack. This is because the stack uses an object to store its elements, and the size of the object grows linearly with the number of elements.

---

## Queues

Picture a queue as a line of people waiting for a ride at an theme park.(*my first thought as someone who grew up playing Roller Coaster Tycoon on my PC*) The first person to get in line is the first person to get on the ride, and new people join the end of the line. This is known as FIFO (First In, First Out) - the first person in the line is the first person to be served.

This code implements a simple queue data structure in JavaScript:

```javascript
class Queue {
	// Constructor for creating a new queue object
	constructor(maxSize){
		this.storage = {}  
		this.head = 0  
		this.tail = 0  
		this.maxSize = maxSize || 10000 
	}

	// Method to add an item to the back of the queue
	enqueue(item){
		if (this.tail >= this.maxSize) {  // If the tail index has reached the maximum size of the queue
			console.log('Queue overflow error')  
			return  // Return without adding the item to the queue
		}
		this.storage[this.tail] = item  
		this.tail++  // Increment the tail index to the next position
		console.log(`Added ${item} to the queue.`) 
	}

	// Method to remove the item at the front of the queue
	dequeue(){
		if (this.head === this.tail) {  // If the head index is the same as the tail index, the queue is empty
			console.log('Queue is empty')  
			return 
		}
		let removed = this.storage[this.head] 
		delete this.storage[this.head] 
		this.head++  // Increment the head index to the next position
		console.log(`Removed ${removed} from queue.`) 
		return removed;  
	}
}
```

### Time/Space Complexity

The time complexity of the `enqueue` and `dequeue` methods in this implementation of a queue is O(1) or constant time. This is because both operations only require accessing and modifying the first or last element of the object, which can be done in constant time regardless of the size of the queue.

The space complexity of the queue implementation is O(n), where n is the number of elements in the queue and the size of the object grows with the number of elements. Therefore, the space required to store the queue elements increases linearly.



So, the biggest difference between a stack and a queue is the way they store and retrieve data. A stack uses LIFO, meaning the most recently added data is the first one to be removed, while a queue uses FIFO, meaning the first data added is the first one to be removed.