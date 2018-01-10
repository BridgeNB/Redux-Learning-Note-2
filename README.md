## Introduction

In this blog I will cover redux fundamentals, including basic concept of redux, three main players of redux and a procedure to build a small redux-react app.

## Table of Contents
1. Introduction of Redux
2. Redux imporves Predictability
3. Redux Stores vs Component State
4. Pure Function
5. Reducer function
6. Redux at its core
7. Create an action
8. Create a reducer
9. Create a Redux store

## Content
### 1. Introduction of Redux
Redux is all about statement managenent. When building web applications, Redux not only organizes the way to store data, it also gives us the ability to quickly obtain that data anywhere within the app. This part is very important that you don't need to pass props through serveral components.
In order to achieve this, Redux build a single object tree to store all global state in a tree.
To maintain this single source of truth, redux app make the state <strong>read-only</strong> and <strong>immutatable</strong>. You have to use intent to update the state.
Typically, proper state management in Redux app should manage data such as <strong>form state</strong>, <strong>server response</strong>, <strong>Cached Data</strong>, and <strong>local data not yet persisted to a server</strong>
### 2. Redux Improves Predictability
Redux use a store to keep all the states so in a nested condition, the app dont need to pass state through a bounch of components. Like this:
![Figure1 nested components without redux.png](quiver-image-url/3EE8345FB30A7385681297E186FCE922.png =274x251)
By apply redux, the app just need to retrieve data from store, which dramatially improves the predictability
![Figure2 nested components with redux.png](quiver-image-url/5D5B1BBC4D94E9113DFE49EC4BE112D1.png =288x318)
Which is also called <strong>unidirectional data flow</strong>.
<strong>Recap</strong>
Redux provide predictability by
- consolidate most data to one location.
- components have to request access to data.
- Data in the store flows in one direction - aka unidirectional data flow.
- Strict rules on how the store can be updated.

### 3. Redux Stores vs Component State
In practise, Component state should store short lived state that doesn't matter the the app globally and doesn't mutate in complex ways，such as a toggle in some UI element or a form input state. On the contrary, Redux should store states which are shared and accessible through the whole app.
<strong>Redux State is Read-only</strong>
The reason why redux state is read only is due to:
- Predictability and reliability is improved
- Side effects are prevented
- The number of external resources writing to state is hindered
- All changes are centralized and happen one-by-one in a strict order
Given an example:
```jsx
/* This is a pure function */
const square = x => x * x;
/* This is not a pure function */
const tipRate = 0.20;
const calculateTip = cost => cost * tipPercentage;
/* Because calculateTip func depends on external parameter tipRate */
```

### 4. Pure Function
What is pure function:
- Return one and the same result if the same arguments are passed in
- Depend solely on the arguments passed into them
- Do not produce side effects
Why use pure function:
- Pure functions are inherently modular, making them easy to test.
- Pure functions make maintaining code much simpler
Learn how to well use pure function would help you to write great functional code.

### 5. Reduce function
What is reduce function
- reduce() will takes in a large amount of data but returns a single value.
Given an example:
```jsx
const iceCreamStats = [
  {
    name: 'Amanda',
    gallonsEaten: 3.8
  },
  {
    name: 'Geoff',
    gallonsEaten: 5.2
  },
  {
    name: 'Tyler',
    gallonsEaten: 1.9
  },
  {
    name: 'Richard',
    gallonsEaten: 7923
  }
];
/*Implement reducer function*/
iceCreamStats.reduce( (accumulator, currentValue) => {
  return accumulator + currentValue.gallonsEaten;
}, 0);
/* In above example, call back function accept two parameters and return one value as result */
```

### 6. Redux at its core
Redux have three major players
- action
- store
- reduce
They are interactive, shown in below image
![Figure3 Redux players.png](quiver-image-url/7FCA3FB92F070EC629CB0FE990BFE21E.png =544x293)

### 7. Create an action
Actions are JS objects that describe an event that should update the application's state.
Given an example:
```jsx
/*Action is a js object with type property */
{
  type: 'EDIT_USER'
  id: 917
}
/*Things to pay attention
 1. Use constants rather than strings as the value of __type__ properties. It is better for debugging.
 2. Keep the payload as small as possible
*/
/* Action creator - function wraps action */
const submitUser = user => ({
  type: SUBMIT_USER,
  user
})
```

### 8. Create a reducer
A reducer is just a function which receives the current state and the specific action which was returned from an action creator.
Given an example:
```jsx
/*Normally, in side of the reducer, we create a if/else statement to match the type property of the action. Then we return a new, updated state*/
function reducer (state, action) {
  switch(action.type) {
    case 'SUBMIT_USER':
      return Object.assign({}, state, {
        user: action.user
    })
  }
}
/* The most import rule to remember here is that your reducer must be a pure action */

/* In a safer way, we add a initial state in case of undefined state such as...*/
function myReducer (state = initialState, action) {
  if (action.type === CHANGE_NAME) {
    return {
      ...state,
      name: 'Tyler'
    };
  }

  return state;
}
/*More example could be viewed in the Udimeal under reducer folders*/
```

### 9. Create a redux store
The redux store will
- holds the app's state
- dispatches actions
- calls reducers
- receives/store new state
<strong>What store will return</strong>
1. getState() - doesn't take any argument and will return the current state of the store
2. dispatch() - dispatch(state) takes in an action object and will call the reducer function, then pass the current state and dispatch the action.
3. subscribe(cb) takes in a listener callback function that will be invoked whenever the state of the store changes.
Given an example:
```jsx
import { createStore } from 'redux'
import reducer from './reducers'

const store = createStore(
  reducer,
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
  /*Use this to invoke redux tool in react view*/
)

ReactDOM.render(<App />, document.getElementById('root'));
registerServiceWorker();

```

## Conclusion
## Code Reference
https://github.com/BridgeNB/Redux-Learning-Note-1
