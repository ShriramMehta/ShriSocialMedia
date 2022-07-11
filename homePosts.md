Que. How to get page no
Ans.
function useQuery() {
return new URLSearchParams(useLocation().search);
}
const query = useQuery();
const page = query.get("page") || 1;

Que. trim in js
Ans. The trim() method removes whitespace from both sides of a string.

The trim() method does not change the original string.

let text = " Hello World! ";
let result = text.trim();
result = Hello World!

Que. useSelector
Ans. useSelector is a function that takes the current state as an argument and returns whatever data you want from it. It’s very similiar to mapStateToProps() and it allows you to store the return values inside a variable within the scope of you functional components instead of passing down as props.
