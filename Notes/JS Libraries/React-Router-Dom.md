# React Router Dom

To install the react router dom we have to do

```shell
npm i react-router-dom
```

<hr>

We have to first wrap the `App` component which is inside the `main.jsx` file in the Router

```jsx
...
import { BrowserRouter } from "react-router-dom";

...
    <BrowserRouter>
      <App />
    </BrowserRouter>
...
```

Then, inside our `App.jsx` we can use the `Routes` and `Route` Component to work with routing, we need to first import them in the app using

```jsx
import { Route, Routes } from 'react-router-dom'
```

then, we can do 

```jsx
<Routes>
    <Route path='/' element={<Home/>} />
    <Route path='/yash' element={<About/>} />
</Routes>
```

This will render the particular component when at the given route, for instance, here in this example, when we are at the `/` route, the `Home` component will be rendered. 

So, `path` takes the route and `element` takes the component or the jsx that is to be rendered

<hr>

### Dynamic Routes

Like we used the `param` or dynamic route in express, we are able to use the same in React Router as well

```jsx
<Route path="/users/:id" element={<Userpage/>} />
```

The `id` will be passed to the component as a paramter and we can render content based on the params passed

```jsx
...
const {id} = useParams()

return (
    <>
        <h1>User {id}</h1>
    </>
)
...
```

We can have multiple parameters as well like `/users/:id/:messageid`

If we have dynamic routes and hardcoded routes that have the same schema, for example

```jsx 
<Route path="/app/:username" element={<User/>} />
<Route path="/app/info" element={<Info/>} />
```

<hr>

### Nested Routes

We can also have nested routes in our react app

```jsx
<Routes>
    <Route path="/books">
        <Route path=":id" element={<Book/>} />
        <Route path="new" element={<NewBook/>} />
    </Route>
</Routes>
```

Now, this works as we expect it to work, but, what if we want to show some default wrapper or component on each page and we want just want the specific content to change, we can do it using

```jsx
<Route path="/books" element={<MainBook/>} >
        <Route path=":id" element={<Book/>} />
        <Route path="new" element={<NewBook/>} />
</Route>
```

but just doing this will not make it work, we need to add an component named `<Outlet/>` wherever we want the nested route code to appear. So in the `<MainBook/>`

```jsx
<>
    <h1>This is a book</h1>
    <div style={{"padding":"20px"}}>0
        <Outlet/>
    </div>
</>
```

We can also wrap all such routes in a parent route without defining the parent's path, it will remove the prefix path but will work the same way using `outlet`

## Redirecting without the \<Link> element

We use `window.location.href` normally to redirect using javascript, but this makes a network request and our page is not changed in a SPA way, to replace it, we can use the `useNavigate` hook


```js
const navigate = useNavigate()
navigate("/dashboard");
```


We cannot invoke or use the `useNavigate` hook outside of the BrowserRouter. Which means, in the general context, we cannot use the useNavigate hook in the App.jsx component directly.