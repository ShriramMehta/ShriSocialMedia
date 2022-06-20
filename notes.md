Que. What is DOM?
Ans.

1. DOM, abbreviated as Document Object Model, is a World Wide Web Consortium standard logical representation of any webpage. In easier words, DOM is a tree-like structure that contains all the elements and it’s properties of a website as its nodes.
2. DOM provides a language-neutral interface that allows accessing and updating of the content of any element of a webpage.

Que. ReactDOM/virtual DOM ?
Ans.

1.  Before React, direct manipulation of the DOM elements used to be done which resulted in frequent DOM manipulation, and each time an update was made the browser had to recalculate and repaint the whole view according to the particular CSS of the page, which made the total process to consume a lot of time.
2.  The Virtual DOM can be referred to as a copy of the actual DOM representation that is used to hold the updates made by the user and finally reflect it over to the original Browser DOM at once consuming much lesser time.
3.  ReactDOM is a package that provides DOM specific methods that can be used at the top level of a web app to enable an efficient way of managing DOM elements of the web page. ReactDOM provides the developers with an API containing the following methods and a few more.

render()
findDOMNode()
unmountComponentAtNode()
hydrate()
createPortal()

Que. render() Function ?
Ans.

1. This function is used to render a single React Component or several Components wrapped together in a Component or a div element. This function uses the efficient methods of React for updating the DOM by being able to change only a subtree, efficient diff methods, etc.

Syntax:

ReactDOM.render(element, container, callback)

element: This parameter expects a JSX expression or a React Element to be rendered.
container: This parameter expects the container in which the element has to be rendered.
callback: This is an optional parameter that expects a function that is to be executed once the render is complete.

eg. ReactDOM.render(<div><App /></div>, document.getElementById("root")

Que. React riuter
Ans. Adding React Router Components: The main Components of React Router are:

BrowserRouter: BrowserRouter is a router implementation that uses the HTML5 history API(pushState, replaceState and the popstate event) to keep your UI in sync with the URL. It is the parent component that is used to store all of the other components.
Routes: It’s a new component introduced in the v6 and a upgrade of the component. The main advantages of Routes over Switch are:
Relative s and s
Routes are chosen based on the best match instead of being traversed in order.
Route: Route is the conditionally shown component that renders some UI when its path matches the current URL.
Link: Link component is used to create links to different routes and implement navigation around the application. It works like HTML anchor tag.
Switch : The switch component looks through all of its child routes and it displays the first one whose path matches the current URL.

This component is what we want to use in most cases for most applications, because we have multiple routes and multiple plate pages in our app but we only want to show one page at a time.

If for some reason you do want multiple pages to be displayed at the same time, you might consider not using the switch component.

Que. Exact param in router :
Ans. The exact param disables the partial matching for a route and makes sure that it only returns the route if the path is an EXACT match to the current url.

Que. Location
Ans. useLocation
The useLocation hook returns the location object that represents the current URL. You can think about it like a useState that returns a new location whenever the URL changes.This could be really useful e.g. in a situation where you would like to trigger a new “page view” event using your web analytics tool whenever a new page loads, as in the following

function usePageViews() {
let location = useLocation();
React.useEffect(() => {
ga.send(["pageview", location.pathname]);
}, [location]);
}

Locations represent where the app is now, where you want it to go, or even where it was. It looks like this:{
key: 'ac3df4', // not with HashHistory!
pathname: '/somewhere',
search: '?some=search-string',
hash: '#howdy',
state: {
[userDefined]: true
}
}

Que. history.push
Ans. We can push users from one page to another using history.push. When we use the push method, we just need to supply the path that we want to take our users to using this method. It adds this new page on to the stack (so to speak) of our history:

Que. URLSearchParams
Ans. help in parsing and accessing query parameters.

For url parameters, like /animals and /cars, you can use the colon syntax /:type

But for query parameters, like ?filter=something, you need to parse the query string.

For example, in your component you will have location as a prop from the parent Route (or you can get it from withRouter), you can then use location.search to parse the query string like this:
URLSearchParams(useLocation().search);
