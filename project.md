1. index.js
   a. store created :
   const store = createStore(reducers, {}, compose(applyMiddleware(thunk)));

   b. render and provider provides stire to the application : ReactDOM.render(
   <Provider store={store}>
   <App />
   </Provider>,
   document.getElementById("root")
   );

2. App.js
   a. check and save user with localstorage

   b. inside browserrouter navbar and then 6 path with exact components.

3. Navbar
   a. Either sign in button or logout div in toolbar

   b. link for img and component

   c. useeffect on location new page changing.
