* Return data from fetch request

```jsx
// ----- fetching inside component: ------

export default function useFetch(URL){

const [data, setData] = useState()
const [id, setId] = useState()

useEffect(() =>{
  async function startFetching(){
    const response = await fetch(URL)
    const data = await response.json()
    
    setData(newData)
  }
  startFetching()
}, [data]);

return data
}


// ----- fetching with custom component: ------

// in the useJoke.js (the use... indicates a custom hook)
export default function useJoke(){
  const [id, setId] = useState()
  const newJoke = useFetch("https://apiurl.here/${id}")
  
  function handleNextJoke(){
    setId(newJoke.nextId);
  }
  
    function handlePreviousJoke(){
    setId(newJoke.prevId);
  }
  
  return {newJoke, handleNextJoke, handlePreviousJoke}  // return an Object; since newJoke : newJoke (and also handleNextJoke) repeats, we can also just write it once
}


// -- in the app.js --
export default function Joke(){
  const [newJoke, handleNextJoke, handlePreviousJoke] = useJoke()  // destructure Object // only works if the names are the same
  
  if(!newJoke){
    return "Loading"
  }
  
  return(
    <>
      <h1>{newJoke.joke}</h1>
      <button typ="button" onClick={handleNextJoke}
      }> Next Joke </button>
      
      <button typ="button" onClick={()=>{
            handlePreviousJoke()            // can also be done with a callback like here (but then needs the ()
        }
      }> Previous Joke </button>
    </>
  )
}
 
```
* we create component and isolate / abstract the data fetching
