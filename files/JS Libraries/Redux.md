# Redux

### Why do we need Redux

Redux is used to make a single store for all the data that will be used in our app. This eliminates the confusion created by a lot of different states and effects. More importantly, our data can be accessed by all the components without any special and/or specific additional commands.

## Redux terms

### Action

An action in redux is a simple javascript object that has a type field to specify what has happened and other fields which gives additional information about the action, about what happened.

For example, if we have a todo app and we want to add an item in the list, we will have an action something like this 

```js
const addTodo = text => {
  return {
    type: 'todos/todoAdded',
    payload: text
  }
}
```

Here, **addTodo** is the name of the function that will return an action, **type** is the name of the action, it is generally the name of the action in the `domain/eventName` format, **payload** is the data that we will use, here, the text that we will put in the todo list. We can also have other fields which will help us to do our desired task

### Reducers 

Reducers are the main place where logic for the actions is stored, we pass the state and action to the reducers, and there, the reducers decide what action to take, reducers first see if the given action is actionable by using if/else or switch statements and then the appropriate action is taken on the state

Reducers should not modify the state, reducer has to copy the state and modify that new variable and then update the state using proper methods.

### Store

The store is where we keep all our data of the redux app. This is the central hub for our data.

We pass the reducers to the store while creating it and we get a `getState()` function which we can use to access the store.



### Dispatch

The dispatch method is provided by the store and the dispatch method is the only way in which we can update the state. 


## Using Redux in React

To use, redux in react, we use `redux-toolkit`

First, we must install **redux** and **redux-toolkit**

```shell
npm i redux
npm i @reduxjs/toolkit
```

Then, we configure a store in **src/app/store.js** or any such dedicated folder. The store is the centre of all the data, it is the single source of truth in the app. 

```js
// store.js

import { configureStore } from "@reduxjs/toolkit"
import todoReducers from "../features/todo/todoSlice.js"

export const store = configureStore({
  reducer: {
    todo: todoReducers
  }
})
```
Here, todoReducers is the reducers that we export from the todoSlice, reducers are the thing that we use to modify the state. A store must get the information about the reducers in order to be created.  

```js
// todoSlice.js

import { createSlice, nanoid } from "@reduxjs/toolkit";

const initialState = {
  todos: [{ id: nanoid(5), text: "Hello world" }],
};

const addTodoFun = (state, action) => {
  const todo = {
    id: nanoid()
    text: action.payload,
  };
  state.todos.push(todo);
};

const removeTodoFun = (state, action) => {
    state.todos = state.todos.filter((todo) => todo.id !== action.payload)
}

export const todoSlice = createSlice({
  name: "todo",
  initialState,
  reducers: {
    addTodo : addTodoFun,
    removeTodo : removeTodoFun
  },
});

export const {addTodo, removeTodo} = todoSlice.actions;
export default todoSlice.reducer;

```

In the above code file, a lot of things are going on, firstly this is the


## Learn more

- [Official Redux Documentation -> https://redux.js.org/tutorials/essentials/part-1-overview-concepts](https://redux.js.org/tutorials/essentials/part-1-overview-concepts)