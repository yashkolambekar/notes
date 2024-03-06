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
arrayOfValues.map((item) => (<li>This is our {item}</li>))
```

So for each value in the array, we will get a li element which says This is our 'value'. 

But, while using map function or other such functions to generate components from list of values, we need to give a `key` prop to each item which helps react in imporving performance while regenerating the componenets if something is changed. <br>
This `key` prop must be unique and discrete!