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

```js
const initialState = { value: 0 }

function counterReducer(state = initialState, action) {
  // Check to see if the reducer cares about this action
  if (action.type === 'counter/increment') {
    // If so, make a copy of `state`
    return {
      ...state,
      // and update the copy with the new value
      value: state.value + 1
    }
  }
  // otherwise return the existing state unchanged
  return state
}
```

### Store