1.  index.js
    a. store created :
    const store = createStore(reducers, {}, compose(applyMiddleware(thunk)));

    b. render and provider provides stire to the application : ReactDOM.render(
    <Provider store={store}>
    <App />
    </Provider>,
    document.getElementById("root")
    );

2.  App.js
    a. check and save user with localstorage

    b. inside browserrouter , switch and then each 6 routes with exact components.

3.  Home
    4 things three components. One left three right.
    i. Left is Posts components with setCurrentID prop which is state initilized to 0.
    ii. Right up is appbar which has one textfield and one chipinput and button.
    a. TextField : value={search}
    onChange={(e) => setSearch(e.target.value)}
    onKeyDown={handleKeyPress}

                     How to handle enter key with textfield:
                     onKeyDown={handleKeyPress}
                      const handleKeyPress = (e) => {
                        if (e.keyCode === 13) {
                        searchPost();
                        }
                        };

    b. ChipInput helps in search in tags. Once you press enter then it gets added to tags array.
    <ChipInput
    style={{ margin: "10px 0" }}
    value={tags}
    onAdd={(chip) => handleAddChip(chip)}
    onDelete={(chip) => handleDeleteChip(chip)}
    label="Search Tags"
    variant="outlined"
    />

    const handleAddChip = (tag) => setTags([...tags, tag]);

    const handleDeleteChip = (chipToDelete) =>
    setTags(tags.filter((tag) => tag !== chipToDelete));

    c. Button onclick calls searchPost which pushes to url with search tags

    const searchPost = () => {
    if (search.trim() || tags) {
    dispatch(getPostsBySearch({ search, tags: tags.join(",") }));
    history.push(
    `/posts/search?searchQuery=${search || "none"}&tags=${tags.join(",")}`
    );
    } else {
    history.push("/");
    }
    };

    iii. Then to form component currentid and setcurrent id is sent whcih sees if user logged in or not.

    iv. And last if searchQuery or tags do not present so show pagination component. with page prop
    How to get page no
    function useQuery() {
    return new URLSearchParams(useLocation().search);
    }
    const query = useQuery();
    const page = query.get("page") || 1;
    ii. SearchQuery : const searchQuery = query.get("searchQuery");

4.  Navbar
    a. Either sign in button or logout div in toolbar

    b. link for img and component

    c. useeffect on location new page changing.

5.  Posts
    if isloading getting from useselector using posts then show cicularprogress else map over posts whcih have found from useselcetor and show post component whith prop setcurrentid and post

6.  Post
    i. inside card and button base calls onclick openPost which pushes to url with post id
    ii. image as post.selectedFirl and title
    iii. to have a month ago : {moment(post.createdAt).fromNow()}
    iv. How to edit the post : check user is same as loogeed in and once clickes on more options stop pagination and set current post id and all the text will apear in form
    v. shwo post tags.with `#{tag}`
    vi. shwo title and 20 words of descriptions and then ...
    {post.message.split(" ").splice(0, 20).join(" ")}...
    vii. Likes compoennt which onclick handleclick
    viii. then if user and post creator are same then shwo delete icon with onclick that disparches deletepost

7.  Likes
    const [likes, setLikes] = useState(post?.likes);

    if user has liked then show something else show like
    const Likes = () => {
    if (likes.length > 0) {
    return likes.find((like) => like === userId) ? (
    <>
    <ThumbUpAltIcon fontSize="small" />
    &nbsp;
    {likes.length > 2
    ? `You and ${likes.length - 1} others`
    : `${likes.length} like${likes.length > 1 ? "s" : ""}`}
    </>
    ) : (
    <>
    <ThumbUpAltOutlined fontSize="small" />
    &nbsp;{likes.length} {likes.length === 1 ? "Like" : "Likes"}
    </>
    );
    }

    return (
    <>
    <ThumbUpAltOutlined fontSize="small" />
    &nbsp;Like
    </>
    );
    };

HanldeClick checks whether already liked and accordingly dislike or like
const userId = user?.result.googleId || user?.result?.\_id;
const hasLikedPost = post.likes.find((like) => like === userId);

const handleLike = async () => {
dispatch(likePost(post.\_id));

      if (hasLikedPost) {
         setLikes(post.likes.filter((id) => id !== userId));
      } else {
         setLikes([...post.likes, userId]);
      }

};

8. Form
   i. currentid is used in here as if it is presnt use useselctor to call find method to find the post withat id and set state post to that post.
   ii. If user doenst exist shoe please sign.
   iii. a normal form with totle description, tags adding same to the one that doen in searching and clear button with differnce being material ui components

9. Pagination
   if page exists dispatch getposts with page no
   get numberofpages from state.posts where it is calculated and set that to count field.

10. PostDetails
    /posts/:postid
