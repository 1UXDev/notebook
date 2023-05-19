## Repetition: Arrays
```jsx
const fruits = ["Sally", "cuba", "cherry", "pineapple" ];
console.log("fruits")

const fruitsCopy = fruits;
fruits.push("apple")
console.log(fruits)
console.log(fruitsCopy) // returns array with apple as well

```
* both are pointing to the same array in the computers memory
* that happens with "pointing" datatypes: arrays and objects
* With primitive types it does not work like that

** Spread Operator 
```jsx
console.log(...fruits)
// its like iterating over every element of the array

const fruitsCopy = [..fruits]
// would not include the apple in the above example
```
* takes elements in the array and copies each of the elements
* so you do not work with the original array or something pointing at the original array but a "real" copy 


# States
We want React to know when to re-render, where to listen for the changes basically, thats why we have **useState**
* "key" helps react to keep track of the elements which might change 

To send data upstream, the Parentelement needs to hold the data 
We create a function to do that
```jsx
const handleAddMovie = (movie) => {
  console.log(...)
  //movies.push(movie)  // will not change the state of the list, since react does not reRender the component this way
  movies.id = uid();    // assign unique ids
  setMovies([...movies, movie]) // tells react to reRender, spread out items of original array, add the new "movie" and return it as a new "original" array
}

// I need to give the Form the Function Call
// When you're ready, call the function, I'll get the data and give it to you
<Form onAddMovie={handleAddMovie} /> // passing the Function as a prop with naming convention like "onClick", "onSubmit",...

// In the Form.js use the onAddMovie
function Form({onAddMovie}){
  onAddMovie(data)
...
}
```

**Scenario: Press delete Button in Sibling-Component to delete something**
```jsx
const handleDeleteMovie = (id) => {
  const newMovies = movies.filter((movie)=> movie.id !== id)  // filter is used because it returns a new array
  // Logic: if the provided id is not the one of the current looped item, include it in your new array
  setMovies(newMovies)   
}

<Movie onDeleteMovie = {handleDeleteMovie} />
```
* function has to be given as a prop to the sibling-component, which holds the data / list

```jsx
// in Movie Component
<button onClick={()=>onDeleteMovie(id)}>

```

## uid Library 
* generates random id of defined length and gives it to component for react to render it

```jsx
import {uid} from "uid"
```



**Sidenote**
If Data comes in as a prop, the Component is not actually responsible for the data, its just a "peek" at the data


