---
layout: post
title: "Redux: Make State Management great again!"
tags:
 -
---
`Redux` was created to make `state management` predictable, providing a single state container and strict rules on how state can be changed. It can be used with any front-end framework, such as `React`, `Angular`, `jQuery`. 

This was based on the principle of Single Source of Truth(Who cares about truth anyways these days 😜)

<img class="img-fluid" src="/as_blog/images/redux.jpeg">

### Installing Redux

```bash
npm install redux #To Install Redux
npm install react-redux #Allow React components to read data from a Redux store, 
#and dispatch actions to the store to update data.
```

### React-Redux Concepts

The Application state is stored in ..... You guessed it right. It's `store`. The Store looks something like this.

```jsx
{
	name: "babyYoda",
	college: "NIFT",
	cute: true,
	graceful: true,
	isAwesome: true
}
```

To change store, you need to dispatch `action,` Actions are plain old javascript object.

```jsx
{ 
  type: 'ADD_CONTACT', //describes why the state change happened
  name: 'James' 
}
```

To tie the store and the action together, we need to write a function, called a reducer.

```jsx
//Look mf, this is a pure function. It return a new state. Previous state is unchanged
function contactsApp(state, action) {
  switch (action.type) {
    case 'ADD_CONTACT':
      return [ ...state,  action.person ]
    default:
      return state
  }
}
```

Action creators are simple functions that return actions.

```jsx
function addContact(person) {
  return {
    type: 'ADD_CONTACT',
    payload: person
  }
}
```

If we have more than one enitity, then it's good that we break them into multiple entity using `combineReducers`

```jsx
const contactsApp = combineReducers({
  addContacts,
  doSomething
})
```

### Creating Store and Counter App

To create the store, we call the `createStore()` function

`Provider`  connect store to our component. It takes the store as an attribute and makes it available to its child component.

The `connect()` function returns a new component, that wraps the component you passed to it and connects it to the store using its special parameter functions.

`mapStateToProps` simply returns the state variables as props to our component, while const Counter = connect(mapStateToProps, mapDispatchToProps)(Counter); allows to define how we dispatch actions and make the dispatching functions available as prop

```jsx
import { Provider } from 'react-redux';
import { createStore } from 'redux';

const initialState = {
  count: 0
};

//World's Nest Action Function. JK 😜
function incrementCounter(num) {
  return { 
    type: 'INCREMENT', 
    num: num 
  }
}

//World's Best Reducer Function
function reducer(state = initialState, action) {
  switch(action.type) {
    case 'INCREMENT':
      return { count: state.count + action.num };
    default:
      return state;
  }
}

const store = createStore(reducer);

const el = <Provider store={store}><Counter/></Provider>; //Connect Store to our Component. i.e Counter

const Counter = connect(mapStateToProps, mapDispatchToProps)(Counter);
```