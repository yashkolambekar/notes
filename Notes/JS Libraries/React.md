# React

To create a react app, we do

```console
npm create vite@latest appname
```

This created a react a new react app with vite, in a newfolder named appname
We can do `npm run dev` to start the server and check our react app in the browser.

We can also use React using a cdn but it is very limiting and not at all recommended but it can be done!

React is basically a declarative way of writing Javscript for the frontend meaning, me tell react what we wan to see on the screen and React does it for us under the hood using javascript

<hr>

Although JSX looks like HTML, but it is not HTML, so some features might be written in a different way.

<hr>

```jsx
const Component = () => {

  console.log("Component added");

  return(
    <>
      <h1>Hello this is a component</h1>
    </>
  )
}

export default Component;
```
This is an example of how component files should be.

<hr>

To use components in our App or within another components we first import the Components in the page using

```jsx
import Appname from "./Components/Appname";
```

And then use them inside our jsx code like

```jsx
...
<center>
  <Appname />
    <div className="container px-4">
    ...
```

<hr>

### Map function

We use map function to create multiple components from an array of values for example,

```jsx
<ul>
  {arrayOfValues.map((item) => (<li>This is our {item}</li>))}
</ul>
```

So for each value in the array, we will get a li element which says This is our 'value'. 

But, while using map function or other such functions to generate components from list of values, we need to give a `key` prop to each item which helps react in imporving performance while regenerating the componenets if something is changed. <br>
This `key` prop must be unique and discrete!

The key is not shown in the final dom but is used in virtual-dom of react

<hr>

### Conditional rendering

We cannot use else if conditions inside jsx because it is an expression and not a code block, so we need to use ternary operators for conditional rendering insdie the jsx.
For example,

```jsx
{someExpression ? <h1>True value</h1> : <h2>False value</h2>}
```

This is how we can use ternary operators inside jsx for conditional rendering it can be used for various interactive ui purposes

We can also use `&&` and `||` for conditional rendering based on the concept of truthy and falsy values. 

## React.memo

If we have a lot of components on the same page and a lot of re-renders are happenig, we do not want every change to trigger a re render, so we use the React.memo 

A *memoised* component will only re-render when the props are changed

```jsx
const Comments = React.memo((title, description) => {
  return (
    <>
    // Content here
    </>
  )
})
```

Now, in the above component, if we have 100 comment components on a page and all are controlled from the parent's state, generally, all will re-render if even one of the comment is changed, but because we are using memo, only the comment whose props are changed will be re-rendered!

> UseMemo and React.memo are different!


## useEffect()

The `useEffect()` hook allows us to perform sideffects which can't/should not be done using rendering.


```js
useEffect(() => {
  // code goes here
}, [])
```

The useEffect hook takes in 2 arguments, the first argument is a function that will run, and the second is the dependency array which contains the states which decides when the useEffect will run.

The main function in the useEffect hook cannot be async function, if we want to have it, we can use an additional library which provides that functionality


## useMemo

useMemo hook is used for memoization of functions, it means, if the inputs of the function are not changing, the function will not be ran and the last output will be given again.

This is useful only for the functions which give consistent output for consistent input, which means, one set of input can produce only one output, no matter when and how many times it runs.

we run useMemo just like use effect, one function and one dependency array

```js
const sum = useMemo(()=> {
  let tempSum = 0;
  for(let i = 0; i <= target; i++){
    tempSum += i;
  }
  return tempSum;
}, [target]);
```

## useCallback 

useCallback is the useMemo for functions!

```js
const getSum = useCallback(() => {
  let tempSum = 0;
  for(let i = 0; i <= target; i++){
    tempSum += i;
  }
  return tempSum;
}, [target])

```

## Lazy Loading

We may not want to send the whole app's code at once to the user as it will increase the overhead and user has to download a lot of unused stuff, to solve this, we can send our app in parts, it is called lazy loading

To use lazy loading, we just have to change the way in which we import the components

```jsx
import {Suspense, lazy} from "react";
const Dashboard = lazy(() => import("../components/Dashboard"));
...
...
...
<div>
  <Routes>
    <Route path="/dash" element={<Suspense fallback={"loading..."}><Dashboard /></Suspense>}>
  </Routes>
<div>
```