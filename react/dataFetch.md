# Data Fetch through SWR

* Usually we trigger an API Fetch even if we have shown the information already
* Better: before we fetch API, we check whether the data is in the Cache / LocalStorage already to load it from there
* Configuration:
   * On pagefocus swr could reload the data everytime
   * refresh on interval ```useSWR(`url${id}`, fetcher, {{refreshInterval:1000}})```
   * mutate -> when data in API is different than in Cache, change cache (but implicit in e.g. refreshIntervall)


### How To
* `npm install swr`
* `import useSwr from "swr"`

**SWR Basics**
```jsx
// ----- The old way -----
// Fetch URL
// turn it to JSON
// useEffect listening to [url] containing an async function that is called immediately (/also works with self-involking function)
// Buttons in return() trigger setId to the appropriate key (each button has their own function)
// error handling and loading animation hast to be done manually

// ------ new way with swr - stale-while-revalidate ------
// Checks the cache and sees what data needs to be loaded from API
// replaces state and fetching, no need for a custom useFetch-hook

export default function Joke() {
  const[id, setId] = useState(0);
  const {data} = useSWR(`https://www.api.com/jokes/${id}`, fetcher)
  // fetcher is a wrapper around the native fetch, a function we can copy from documentation, name is egal
  // benefit of fetcher-wrapper : make fetch-function from JS my own function ("fetcher") and give it new to-do`s, e.g. adding a console.log
  // key for data in cache will be the string in useSWR
}

// --- in _app.js ---
// as placeholder for whatever page is rendered, if you add an element (e.g. Nav or H1), that will appear on every page
import {SWRconfig} from "swr"

// add fetcher function 
 const fetcher = (...args => {
      // here could be a console.log() - if its only the default line, we can skip curly-brackets
      fetch (...args).then(res=> res.json())
      }

return(
  <App>
    <SWRconfig value={{fetcher}}>
      <Component {...pageProps}>
    </SWRconfig>
  </App>
)

```

<br>

**Errorhandling and Loading with SWR**
```jsx
...

export default function App(){
const {data,error,isLoading} = useSWR("https://api.github.com/repos/vercel/swr", fetcher) // destructure the object
  if (error) return "An error has occured"
  if (isLoading) return "Loading..."
  
return ( 
  ...
)}
```

if we e.g. want to append an emoji to the jokes, that you can toggle to classify the joke as funny:
* we have to keep a seperate object-array that stores which joke was funny and which was not
* on the first click:
  * is there an Object with the clicked ID?
    * YES: we change isFunny to false
    * NO: we ass an Obj. to array with funny = true
```jsx
// --- setting the Emoji in the DOM, depending on the array
const info = jokesInfo.find((info)=> info.id === id) ?? {isFunny:false}; //if this is undefined, set isFunny to false
const {isFunny} = info;
...
<my element>
  <p aria-label={isFunny ? "A laughing face" : "a bored face"} >
      {isFunny ? 🤣 : 😒}
  </p>
```

```jsx
// --- function to check if joke exists in array already
// check if joke is in Array
function checkJoke(){
const info = JokesInfo.find(...)
if (info){
  return jokesInfo.map((info)=>{
    info.id === id ? {...info, isFunny: !info.isFunny}
  } 
  // if joke is not already in the array, return the old array with the current clicked joke appended
  return [...jokesInfo, {id, isFunny:true}]
}; 
}
``` 

