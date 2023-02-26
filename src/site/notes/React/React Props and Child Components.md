---
{"dg-publish":true,"permalink":"/react/react-props-and-child-components/"}
---


# Passing Props From Parent to Child Components

----
02-25-2023

React props are a way to pass data and functionality from one component to another in a React application. They allow you to customize and configure a component with specific values or functions.

When you create a component in React, you can define its props by adding attributes to the component tag. In this code, props are being passed to three different components: Header, Content, and Total.

```jsx
// Necessary imports in order to render the components inside of App.jsx
import Header from "./components/Header"
import Content from "./components/Content"
import Total from "./components/Total"

const App = () => {

	const course = {
		name: 'Half Stack application development',
		parts: [
			{
				name: 'Fundamentals of React',
				exercises: 10
			},
			{
				name: 'Using props to pass data',
				exercises: 7
			},
			{
				name: 'State of a component',
				exercises: 14
			}
		]
	}

	return (
		<div>
			<Header className='courseHeader' course={ course } />
			<Content courseMaterial={ course.parts }/>		
			<Total exercises={ course.parts }/>
		</div>
	)
}
```

The Header component is receiving a prop called "course", which is an object containing the name of the course and an array of parts. This prop is passed to Header as an attribute and accessed from the Header component in a Header.jsx

```jsx
const Header = ({ course }) => {
	return (
		<header>
			<h1>{ course.name }</h1>
		</header>
	)
}
// Export allows the Header component to be rendered in App.jsx
export default Header
```

The Content component is receiving a prop called "courseMaterial", which is an array of parts from the course object. This prop is also passed to Content as an attribute:

```jsx
// To render the Part component
import Part from "./Part"

const Content = ({ courseMaterial }) => {
	return (
		<section>
		<Part name={ courseMaterial[0].name } exercises={ courseMaterial[0].exercises }/>
		<Part name={ courseMaterial[1].name } exercises={ courseMaterial[1].exercises }/>
		<Part name={ courseMaterial[2].name } exercises={ courseMaterial[2].exercises }/>
		</section>
	)
}  
export default Content
```

```jsx
const Part = ({ name, exercises } ) => {
	return (
// A fragment <></> is a common pattern for a component to return multiple elements. Fragments let you group a list of children without adding extra nodes to the DOM like a <div>.
		<>
			<h3>{ name }</h3>
			<p>{ exercises }</p>
		</>
	)
}
// exporting the grandchild component to be used inside the parent component Content.jsx and then inside App.jsx 
export default Part
```

Finally, the Total component is receiving a prop called "exercises", which is the same array of parts from the course object. This prop is also passed as an attribute:

```jsx
const Total = ({ exercises }) => {
// Javascript methods can be performed inside components to transform the data passed from the props.
	return (
		<h3>Total # of exercises: { exercises.map(part => part.exercises).reduce((a, b) => a + b, 0) }</h3>
	)
}
export default Total
```

In each of these cases, the props are passed as attributes to the component tags. The components can then access these props using the "props" object, which is passed as an argument to the component function. For example, the Header component might access the "course" prop like this as well:

```jsx
const Header = (props) => {
  return <h1>{props.course.name}</h1>;
}
```

One important thing to take away from parent and child component relationships in React is that they are a fundamental way of structuring your application and breaking it down into smaller, reusable pieces.

By dividing your application into parent and child components, you can create a hierarchy of components that can be composed and reused in different parts of your application. This can make your code easier to read, debug, and maintain, as each component is responsible for a specific piece of functionality.

Additionally, passing data and functionality down from parent components to child components via props can help to ensure that your components are decoupled and flexible. This means that you can change the behavior of your components without affecting other parts of your application. 

By breaking your application down into smaller components, you can reduce the amount of unnecessary rendering that occurs and make your application more efficient.