# Fetching Data with react
```jsx
export default function Joke(){
  const[jokeObj, setJokeObj] = useState("");
  const[id, setId] = useState(0);
  
  useEffect(()=>{     // first Parameter callback, second is Array to keep Variables
    function fetchJoke(){
      const response = await fetch(`https://www.google.com/${id}`)
      const data = await response.json()
      
      setJokeObj(data)    // putting the output into the joke Variable, better to safe the whole object instead of just the textcontent, we might need it later
    }
    fetchJoke()     // Call the function inside of useEffect
  },
  [id] ) // keep track of id, whenever id changes, re-render 
  // with an empty array it will just run once, if theres nothing it will loop endlessly
  
  return(
    <>
    {JSON.stringify(jokeObj)}    // JSON to usable object
      <h1>{jokeObj.joke}</h1>    // access the joke atribute of the obj which contains the text
      <button type="button" onClick={()=>{
        setId(jokeObj.nextId)    // on button click, set the id via setter-function to the value of the API-Items attribute "nextId"
       }
      }>Next Joke</button>
    </>
}
```
**ALL APIs should be used in a useEffect container**
