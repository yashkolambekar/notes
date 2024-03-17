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