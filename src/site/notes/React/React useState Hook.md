---
{"dg-publish":true,"permalink":"/react/react-use-state-hook/"}
---


# React `useState` Hook & Immutable State

---

03-09-2023

`useState` is a hook in React that allows you to add state to your functional components. It is used when you need to store and manage state data in your application, such as user input, API responses, or to show/hide components.

In React, state refers to the data that determines the behavior of your application and can change over time. By using `useState`, you can define a piece of state data and a function that updates that data. When the state data is updated, React automatically re-renders the component and any child components that depend on that data. 

>When state data changes in a component, React uses its virtual DOM to determine what parts of the real DOM need to be updated. React compares the previous state of the virtual DOM with the current state to identify any differences. This process is known as reconciliation.

Here's an example of using the `useState` hook to manage the visibility of a modal dialog box:

```jsx
import React, { useState } from 'react';

function ModalButton() {
	const [showModal, setShowModal] = useState(false);

	const handleOpenModal = () => setShowModal(true);
	const handleCloseModal = () => setShowModal(false);

	return (
		<div> {/* always visible */}
			<button onClick={handleOpenModal}>Open Modal</button>
	{/* expression must evaluate to true && true to show */}
			{showModal && (
				<> 
					<div>
						<h2>Modal Title</h2>
						<p>Modal content goes here</p>
						<button onClick={handleCloseModal}>Close</button>
					</div>
				</>
			)}
		</div>
	);
}
```

> An event handler() is supposed to be either a _function_ or a _function reference_. A _function_ _call_ will not work here.

- When the "Open Modal" button is clicked, `handleOpenModal` function is called and updates the `showModal` state data by calling `setShowModal(true)`. This causes the modal dialog box to be displayed, since `showModal` is now `true`.

- When the "Close" button in the modal dialog box is clicked, `handleCloseModal` is called and updates the `showModal` state data by calling `setShowModal(false)`. This causes the modal dialog box to be hidden again, since `showModal` is now `false`.


## Mutable & Immutable State

---

When working with the `useState` hook, it's important to understand the difference between mutable and immutable state. Mutable state is state that can be changed directly, while immutable state is state that cannot be changed directly but must be replaced with a new version.

In React, it's generally recommended to use immutable state as much as possible, as it helps to avoid bugs and make your code more predictable. This means that instead of directly modifying state, you should create a new copy of the state with the desired changes.

Let's say we have a simple React component that displays a list of items and allows the user to add new items to the list. We could implement this component with either mutable or immutable state.

Here's an example of the component using mutable state:

```jsx
import React, { useState } from 'react';

function MutableList() {
  const [items, setItems] = useState(['First Item']);

  function handleAddItem() {
    items.push('New Item'); {/* Directly modifying the state array */}
    setItems(items); // {/* Updating the state with the modified array */}
  }

  return (
    <div>
      <ul>
        {items.map(item => (
          <li key={Math.random()}>{item}</li>
        ))}
      </ul>
      <button onClick={handleAddItem}>Add Item</button>
    </div>
  );
}
```

> We directly modify the `items` array by using the `push` method to add a new item. This can lead to unexpected behavior and bugs, especially if other components are also modifying the same array.

And here's an example of the same component using immutable state:

```jsx
function ImmutableList() {
  const [items, setItems] = useState([]);

  function handleAddItem() {
{/* Use the spread syntax (...) and make a copy of the original state */}
    const newItems = [...items, 'New Item']; 
    setItems(newItems); {/* Update the state with the new array */}
  }

  return (
    <div>
      <ul>
        {items.map(item => (
          <li key={Math.random()}>{item}</li>
        ))}
      </ul>
      <button onClick={handleAddItem}>Add Item</button>
    </div>
  );
}
```

- In the immutable example, we create a new array `newItems` by spreading the existing `items` array and adding the new item to the end. By doing this, all the references of `items` won't be affected until we use `setItems`, and thus changes made to the state are predictable and consistent.

Overall, using immutable state gives you control over your code, helps to avoid bugs, and makes your code more maintainable.