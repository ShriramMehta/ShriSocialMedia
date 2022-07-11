Que. what is redux?
Ans.

1. Redux is a predictable state container for JavaScript apps.
2. As the application grows, it becomes difficult to keep it organized and maintain data flow. Redux solves this problem by managing application’s state with a single global object called Store.
3. Redux fundamental principles help in maintaining consistency throughout your application, which makes debugging and testing easier

Que. Principles of redux :
Ans.

1. Single Source of Truth
   The state of your whole application is stored in an object tree within a single store. As whole application state is stored in a single tree, it makes debugging easy, and development faster.

2. State is Read-only
   The only way to change the state is to emit an action, an object describing what happened. This means nobody can directly change the state of your application.

3. Changes are made with pure functions
   To specify how the state tree is transformed by actions, you write pure reducers. A reducer is a central place where state modification takes place. Reducer is a function which takes state and action as arguments, and returns a newly updated state.

Que. What is an action?
Ans.

1. An action is a plain object that describes the intention to cause change with a type property.

2. It must have a type property which tells what type of action is being performed. The command for action is as follows −

return {
type: 'ITEMS_REQUEST', //action type
isLoading: true //payload information
}

3. Types should be defined as string constants in your application as given below −

const ITEMS_REQUEST = 'ITEMS_REQUEST';

4. Actions are the only source of information for the store as per Redux official documentation. It carries a payload of information from your application to store.

5. To cause any change in the store, you need to dispatch an action first by using store.dispatch() function. The action object is as follows −

{ type: GET_ORDER_STATUS , payload: {orderId,userId } }
{ type: GET_WISHLIST_ITEMS, payload: userId }

Que. What is reducer?
Ans.

Reducers are a pure function in Redux. Pure functions are predictable. Reducers are the only way to change states in Redux. It is the only place where you can write logic and calculations. Reducer function will accept the previous state of app and action being dispatched, calculate the next state and returns the new object.

1. Let us assume our application’s state is described by a plain object called initialState which is as follows −

const initialState = {
isLoading: false,
items: [],
hasError: false
};

2. Every piece of code in your application cannot change this state. To change the state, you need to dispatch an action.

3. Actions and states are held together by a function called Reducer. An action is dispatched with an intention to cause change.

4. This change is performed by the reducer. Reducer is the only way to change states in Redux, making it more predictable, centralised and debuggable.
   A reducer function that handles the ‘ITEMS_REQUEST’ action is as follows −

const reducer = (state = initialState, action) => { //es6 arrow function
switch (action.type) {
case 'ITEMS_REQUEST':
return Object.assign({}, state, {
isLoading: action.isLoading
})
default:
return state;
}
}

5. Redux has a single store which holds the application state. If you want to split your code on the basis of data handling logic, you should start splitting your reducers instead of stores in Redux.

6. The following few things should never be performed inside the reducer −

Mutation of functions arguments
API calls & routing logic
Calling non-pure function e.g. Math.random()
The following is the syntax of a reducer −

(state,action) => newState

Que. Data flow in redux:
Ans.

1. Redux follows the unidirectional data flow. It means that your application data will follow in one-way binding data flow.
   An action is dispatched when a user interacts with the application.

2. The root reducer function is called with the current state and the dispatched action. The root reducer may divide the task among smaller reducer functions, which ultimately returns a new state.

3. The store notifies the view by executing their callback functions.

4. The view can retrieve updated state and re-render again.

Que. Store
Ans.

1. store is an immutable object tree in Redux. A store is a state container which holds the application’s state. Redux can have only a single store in your application. Whenever a store is created in Redux, you need to specify the reducer.

2. Let us see how we can create a store using the createStore method from Redux. One need to import the createStore package from the Redux library that supports the store creation process as shown below −

import { createStore } from 'redux';
import reducer from './reducers/reducer'
const store = createStore(reducer);
A createStore function can have three arguments. The following is the syntax −

createStore(reducer, [preloadedState], [enhancer])
A reducer is a function that returns the next state of app.
A preloadedState is an optional argument and is the initial state of your app.
An enhancer is also an optional argument. It will help you enhance store with third-party capabilities.

3. A store has three important methods as given below −

getState
It helps you retrieve the current state of your Redux store.

The syntax for getState is as follows −

store.getState()
dispatch
It allows you to dispatch an action to change a state in your application.

The syntax for dispatch is as follows −

store.dispatch({type:'ITEMS_REQUEST'})
subscribe
It helps you register a callback that Redux store will call when an action has been dispatched. As soon as the Redux state has been updated, the view will re-render automatically.

The syntax for dispatch is as follows −

store.subscribe(()=>{ console.log(store.getState());})
Note that subscribe function returns a function for unsubscribing the listener. To unsubscribe the listener, we can use the below code −

const unsubscribe = store.subscribe(()=>{console.log(store.getState());});
unsubscribe();

Que. What is pure function and why it is needed is redux?
Ans.

1. A function is called pure if it abides by the following rules −

A function returns the same result for same arguments.

Its evaluation has no side effects, i.e., it does not alter input data.

No mutation of local & global variables.

It does not depend on the external state like a global variable.

2. state.isAddedToCart = !state.isAddedToCart; //original object altered
   Redux compares old and new objects by the memory location of both the objects. It expects a new object from reducer if any change has happened. And it also expects to get the old object back if no change occurs. In this case, it is the same. Due to this reason, Redux assumes that nothing has happened.

So, it is necessary for a reducer to be a pure function in Redux. The following is a way to write it without mutation −
...state,
isAddedToCart: !state.isAddedToCart

Que. Middleware?
Ans.

1. Redux itself is synchronous, so how the async operations like network request work with Redux? Here middlewares come handy. As discussed earlier, reducers are the place where all the execution logic is written. Reducer has nothing to do with who performs it, how much time it is taking or logging the state of the app before and after the action is dispatched.

2. In this case, Redux middleware function provides a medium to interact with dispatched action before they reach the reducer. Customized middleware functions can be created by writing high order functions (a function that returns another function), which wraps around some logic. Multiple middlewares can be combined together to add new functionality, and each middleware requires no knowledge of what came before and after. You can imagine middlewares somewhere between action dispatched and reducer.

3. Commonly, middlewares are used to deal with asynchronous actions in your app. Redux provides with API called applyMiddleware which allows us to use custom middleware as well as Redux middlewares like redux-thunk and redux-promise. It applies middlewares to store. The syntax of using applyMiddleware API is −

applyMiddleware(...middleware)
And this can be applied to store as follows −

import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers/index';
const store = createStore(rootReducer, applyMiddleware(thunk));

4. Conditional dispatch can be written inside middleware. Each middleware receives store’s dispatch so that they can dispatch new action, and getState functions as arguments so that they can access the current state and return a function. Any return value from an inner function will be available as the value of dispatch function itself.

The following is the syntax of a middleware −

({ getState, dispatch }) => next => action
The getState function is useful to decide whether new data is to be fetched or cache result should get returned, depending upon the current state

Que. React redux?
Ans.

1. Let us say if various react components need to display the same data in different ways without passing it as a prop to all the components from top-level component to the way down. It would be ideal to store it outside the react components. Because it helps in faster data retrieval as you need not pass data all the way down to different components.

Let us discuss how it is possible with Redux. Redux provides the react-redux package to bind react components with two utilities as given below −

Provider
Connect
Provider makes the store available to rest of the application. Connect function helps react component to connect to the store, responding to each change occurring in the store’s state.

STORE − Stores all your application state as a JavaScript object

PROVIDER − Makes stores available

CONTAINER − Get apps state & provide it as a prop to components

COMPONENT − User interacts through view component

ACTIONS − Causes a change in store, it may or may not change the state of your app

REDUCER − Only way to change app state, accept state and action, and returns updated state.

However, Redux is an independent library and can be used with any UI layer. React-redux is the official Redux, UI binding with the react. Moreover, it encourages a good react Redux app structure. React-redux internally implements performance optimization, so that component re-render occurs only when it is needed.

To sum up, Redux is not designed to write shortest and the fastest code. It is intended to provide a predictable state management container. It helps us understand when a certain state changed, or where the data came from.

Que. Compose
Ans.

Improved readability and convenience are the main advantages of using compose.

Compose is used when you want to pass multiple store enhancers to the store. Store enhancers are higher order functions that add some extra functionality to the store. The only store enhancer which is supplied with Redux by default is applyMiddleware however many other are available.

Store Enhancers are Higher Order Functions

What are higher order functions? Paraphrased from the Haskell docs:

Higher order functions can take functions as parameters and return functions as return values. A function that does either of those is called a higher order function

From the Redux docs:

All compose does is let you write deeply nested function transformations without the rightward drift of the code. Don’t give it too much credit!

So when we chain our higher order functions (store enhancers) instead of having to write

func1(func2(func3(func4))))
we could just write

compose(func1, func2, func3, func4)
These two lines of code do the same thing. It is only the syntax which differs.

Que. Thunk
Ans. redux-thunk lets the action creators invert control by dispatching functions. They would receive dispatch as an argument and may call it asynchronously. Such functions are called thunks

Redux Thunk is middleware that allows you to return functions, rather than just actions, within Redux. This allows for delayed actions, including working with promises.

One of the main use cases for this middleware is for handling actions that might not be synchronous, for example, using axios to send a GET request. Redux Thunk allows us to dispatch those actions asynchronously and resolve each promise that gets returned.

Once Redux Thunk has been installed and included in your project with applyMiddleware(thunk), you can start dispatching actions asynchronously.
