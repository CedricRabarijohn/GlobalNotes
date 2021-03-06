. En cas d'erreur avec npm install :
    npm install --save /*leh package misy erreur*/ --legacy-peer-deps
. npx clear-npx-cache
. Create the app : npx create-react-app appName
. Run the app : npm run start
. Use "className" instead of "class" in jsx:
    - ex : <div className="content"> Content here </div>
. Dynamic values :
    - ex : const title = 'welcome'
            . inside the jsx : <h1>{ title }</h1>
. Multiple components :
    - create a component (simple js file) ex : GameList.jsx
    - To add it to a jsx, just import it like this : import GameList from './GameList';
        Then place it like this : <GameList></GameList> OR like this <GameList />
. Adding styles :
    - import '**css file location**'
    - If you wanna include style inside jsx, do it inside double braces : //Don't use "-" , for example border-radius should be "borderRadius"
        <div style={{ color:"white", backgroundColor:"red" }}></div>
. Click event:(Simple)
    -  create a function handleClick then link it to a button or whatever should listen to the event :
        const handleClick() = () => {
            //codes here
        }
        .inside the jsx : <button onClick={handleClick}>Click me</button> //handleClick without the parenthesis, otherwise it will 
                                                                            call the function even if the click event didn't happen
. Click event with a parameter :
    - function which will handle the click event :
        const handleClick2() = (parameter) => {
            //codes here
        }
        .inside the jsx :
            <button onClick={ (someParamHere) => { handleClick2(someParamHere) } }>Click me</button>

. Using state (UseState hook) :
    const[name, setName] = useState('mario');
    const changeName = () => {
        setName('luigi')
    }

. Outputting Lists :
    const[games, setGames] = useState([
        {id:1, title:'titre1', description:'description1'},
        {id:2, title:'titre2', description:'description2'},
        {id:3, title:'titre3', description:'description3'}
    ])

    .inside the jsx : (use the map method of javascript) //DON'T FORGET THE KEY (JEREO TSARA LEH CODE)
        {games.map((game) => (
            <div class="game-preview" key={game.id}>
                <h2> {game.title} </h2>
            </div>
        ))}

. Props :
    . It's like a parameter to a component in react
    . How to use it : 
        o Method one : Not destructured
            ex : - Name of the component : GameList
            - inside the jsx where we want to use our component :
                <GameList games={games} title="All games"/>
                
            - inside the parameter of the component function used to create the component itself, use the prop method
                        const GameList = (prop) => {
                            const games = prop.games
                            const title = prop.title
                            return (
                                <>
                                    <div className="title">
                                        {prop.title}
                                    </div>
                                    {games.map((game) => (
                                        <div className="gameContent">
                                            Title : {game.title}
                                        </div>
                                    ))}
                                    
                                <>
                            )
                        }
                        export default GameList;
. Reusing components :
    - Why : 
        . For example , you only want the game who got the key 1
    - How : Use the filter method of javascript
        <GameList games={games.filter(game => game.id ==== 1)} title="All games"/>
. Functions as props : (delete function)
    const handleDelete = (id) => {
        const newGames = games.filter(game => game.id !== id)
        setGames(newGames)
        //code here...
    }
    <GameList handleDelete={handleDelete} />
. UseEffect hook : (basic)
    . Why : do something like for example refresh the data when something changes
    . How :
        .without brackets, it will trigger everytime a data changes inside the component
        useEffect(()=>{
        })
. UseEffect dependencies :
        . Without data to watch inside the brackets, it will only trigger on the first render of the page
            useEffect(()=>{
            }, [])
        . With data to watch :
            useEffect(()=>{
                //some codes
            }, [name])

. Using JSON server :
    - create new file .json: ex : data/db.json
    - inside db.json :
        {
            "games":[
                {
                    "id":1,
                    "title":"First game",
                    "description":"This is the first game"
                },
                {
                    "id":2,
                    "title":"Second game",
                    "description":"This is the second game"
                }
            ]
        }
    
    - Create a new Terminal
    - Run the following command : (ex: the data is inside data/db.json)
        . npx json-server --watch data/db.json --port 8000

. Fetching Data with useEffect :
    useEffect(()=>{
        fetch('http://localhost:8000/games')
        .then(res => {
            return res.json();
        })
        .then(data => {
            console.log(data)
        })
    }, [])

    -To avoid error from null data, use "games && ..."

. Adding bootstrap to react app:
    - npm install bootstrap
    - Go to App.js and import the following :
        . import 'bootstrap/dist/css/bootstrap.min.css' (voir dans node_modules)

. Conditional loading message :
    const[isPending, setIsPending] = useState(true)

    . inside the jsx :
        { isPending && <div>Loading...</div> }
    
    . To simulate the loading, use:
        setTimeout(() => {
            fetch etc...
        }, 1000)

. Handling Fetch Error :
    add a catch after the last "then" when fetching the datas

. Making a custom hook :
    - custom hook should start with "use":
        ex : useFetch()
    - create a new js file named useFetch()
    - const useFetch = (url) => {
        ***useState of datas, isPending and err*** here
        useEffect(() => {
            //same code as usual useEffect but , the url is inside the brackets of useEffect
        },[url])
        return { datas, isPending, err }
    }
    - inside the GameList for example :
        const { datas: games, isPending, err} = useFetch(url);

/*****************************************************************************************
. NEW VERSION OF REACT ROUTER : (V6)
    . npm install react-router-dom@6
    . import { BrowserRouter as Router, Route, Routes} from 'react-router-dom';
    <Router>
        <Routes>
            <Route path="/" element={<Home />}/>
        </Routes>
    </Router>
/*****************************************************************************************
. Router Links :
    - Using it prevents the app to send too much requests to the server
    - import { Link } from 'react-router-dom'
    - Instead of using <a href="blabla"></a> , use instead :
        . <Link to="/">Home</Link>
        . <Link to="/blabla">Blabla</Link>

/***************************************************************************************

. UseNavigate :
    import { useNavigate } from "react-router-dom"

    let navigate = useNavigate();

    - inside the jsx :
        <button onClick={() => {navigate("/")}}>Go to home</button>

. React router useParams (V6) : (ex : We're using the profile component to take params)
    - usage of ":" followed by the params

    <Route path="/profile/:username" element={<Profile />} />

    .inside the Profile Component :
        import { useParams } from "react-router-dom"
        let { username } = useParams()

. Nested Routes (React Router Dom V6) :
    Route inside Route:
        ex : 
            <Route path="/products/" element={ <Products /> }>
                <Route path="/products/list" element={ <ListProducts />} />
            </Route>
        
        . Inside Products : ( Don't forget the <Outlet /> tag )
            <nav>
                Link to blablabla...
            </nav>

            <Outlet />
. React bootstrap : https://www.youtube.com/watch?v=0wJCxEDDetE
    - npm install react-bootstrap bootstrap@4.6.0
. Protected Routes : (To watch : https://www.youtube.com/watch?v=qnH5KNtRYEI&list=RDCMUC8S4rDRZn6Z_StJ-hh7ph8g&index=5 )

. React Hooks : https://www.youtube.com/watch?v=LlvBzyy-558
    - useState
    - use Effect
    - useReducer
    - useCallback
    - useMemo
    - useRef
    - useImperativeHandle
    - useLayoutEffect
    - useDebugValue

. AOS : SCROLL ANIMATION EFFECT IN REACT https://avimistry4800.medium.com/how-to-use-aos-scroll-animation-effect-in-react-ed822190a644
    - npm i aos --save
    - Imports :
        import AOS from "aos";
        import "aos/dist/aos.css";
    - Initialization :
        useEffect(() => {
            AOS.init();
            AOS.refresh();
        }, []);
    - Example of use : <div data-aos="fade-up"
                        data-aos-easing="linear"
                        data-aos-duration="500">
                        </div>
    -Site https://michalsnik.github.io/aos/

. Material UI :
    - installation : npm install @material-ui/core --force
                     npm install @material-ui/icons --force
                     npm install @mui/material @emotion/react @emotion/styled
    - import from @mui/material

. Deploy on heroku w json server
    . install heroku
    . login heroku
    . create Procfile: 
        web: node server.js
    . create server.js file
    .   const jsonServer = require('json-server');
        const server = jsonServer.create();
        const router = jsonServer.router('./db.json');
        const middlewares = jsonServer.defaults({
        static: './build'
        });
        const PORT = process.env.PORT || 8000;
        server.use(middlewares);
        server.use(jsonServer.rewriter({
        '/api/*': '/$1',
        }))
        server.use(router);
        server.listen(PORT, () => {
        console.log('Server is running');
        });

. fetch method javascript : https://www.youtube.com/watch?v=cuEtnrL9-H0
