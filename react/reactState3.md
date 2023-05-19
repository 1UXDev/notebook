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

## Repetition: Spread Operator 
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
### When .map is used (e.g. to toggle a button)
* create new element

```jsx
const newmovies = movie.map((movie)=>{
  const newMovie = {...movie} 
  if (newMoview.id === id){
    newMovie.isLiked = !movie.isLiked;
  }
  return newMovie
}

setMovies(newMovies)
  
  
// Short Version for the above
const newMovie = 
  movie.id === id ? {...movie, isLiked: !movie.isLiked} : movie;
```

## uid Library 
* generates random id of defined length and gives it to component for react to render it

```jsx
import {uid} from "uid"
```

--------------------

**Sidenote**
If Data comes in as a prop, the Component is not actually responsible for the data, its just a "peek" at the data

<br>

<br>

--------------------

<br>


# React State 3

## Learning Objectives

- [ ] Knowing how to handle arrays and objects in state
- [ ] Knowing what state mutation is and how to avoid it

---

## Avoiding State Mutation

Regardless of how complex the state you have in your application (object, array, array of objects) is, you must always treat state as immutable.
This means that you should not directly mutate the state, e.g. with reassigning a new value to it.

To avoid mutation when updating state, you need to

1. create a new object / array (or make a copy of the existing one), and
2. use the setter function with the recently created / updated copy in order to cause a re-render.

---

## Updating Objects in State

To make a copy of an object and change only some properties, you can use the spread syntax:

```js
const [person, setPerson] = useState({
  firstName: "John",
  lastName: "Doe",
});

function handleChangeFirstName(firstName) {
  setPerson({ ...person, firstName });
}

// Somewhere else:
handleChangeFirstName("Jane");
```

> ❗️ If you were to assign a new value directly, you would mutate the state. This is bad because we must treat state as immutable. Doing so can lead to hard to find bugs.
>
> ```js
> // ⚠️ NEVER DO THIS
> function handleChangeFirstName(firstName) {
>   person.firstName = firstName;
>   setPerson(person);
> }
> ```

> 📙 Learn more about [**Updating Objects in State** in the React Docs](https://react.dev/learn/updating-objects-in-state).

---

## Updating Arrays in State

As you know, there are several ways to update arrays. Some of them, however, mutate the array, and some
of them don't.

|           | avoid (mutates the array)           | prefer (returns a new array) |
| --------- | ----------------------------------- | ---------------------------- |
| adding    | `push`, `unshift`                   | `[...arr]` spread syntax     |
| removing  | `pop`, `shift`, `splice`            | `filter`                     |
| replacing | `splice`, `arr[i] = ...` assignment | `map`                        |
| sorting   | `reverse`, `sort`                   | copy the array first         |

> 💡 It does not matter whether your array state contains only primitives or other objects / arrays;
> in all cases, you should only use the preferred array methods.

### Adding to an Array

To add an element to an array, you can use the spread syntax:

```js
const [numbers, setNumbers] = useState([0, 1, 2]);

function handleAppendNumber(number) {
  setNumbers([...numbers, number]);
}

// Somewhere else:
handleAppendNumber(3);

function handlePrependNumber(number) {
  setNumbers([number, ...numbers]);
}

// Somewhere else:
handlePrependNumber(-1);
```

### Removing from an Array

To remove an element from an array, you can use the `filter` method:

```js
const [numbers, setNumbers] = useState([0, 1, 2]);

function handleRemoveNumber(numberToRemove) {
  setNumbers(numbers.filter((number) => number !== numberToRemove));
}

// Somewhere else:
handleRemoveNumber(1);
```

### Replacing an Array Element

To replace an element in an array, you can use the `map` method:

```js
const [numbers, setNumbers] = useState([0, 1, 2]);

function handleReplaceNumber(oldNumber, newNumber) {
  setNumbers(
    numbers.map((number) => {
      if (number === oldNumber) return newNumber;
      return number;
    })
  );
}

// Somewhere else:
handleReplaceNumber(1, 1337);
```

### Sorting an Array

To sort an array, you can use the spread syntax to make a copy of the array first, then sort the copy:

```js
const [numbers, setNumbers] = useState([12, 2, 42, 4]);

function handleSortNumbers() {
  setNumbers([...numbers].sort());
}
```

> 📙 Learn more about [**Updating arrays without mutation** in the React Docs](https://react.dev/learn/updating-arrays-in-state#updating-arrays-without-mutation).

---

## Updating Arrays of Objects in State

Most of the time, you will encounter arrays of objects in your state.

### Adding a new Object

You can add a new object to the state array by using the spread syntax:

```js
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleAddTree(tree) {
  setTrees([...trees, tree]);
}

// Somewhere else:
handleAddTree({id: 3, name: "Spruce", height: 13})
```

### Removing an Object

To remove an object, you can `filter` the array for a unique identifier. In most cases, this
identifier is in scope because the relevant object is rendered via `map`.

```js
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleRemoveTree(idToRemove) {
  setTrees(trees.filter((tree) => tree.id !== idToRemove));
}

// Somewhere else:
handleRemoveTree(0);
```

### Replacing an Object

To replace an object, you can use `map` to create a new array with the updated object. Remember to create a copy of the object first, otherwise you will mutate the state.

```js
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleSetNewHeightForTree(id, height) {
  setTrees(
    trees.map((tree) => {
      if (tree.id === id) return { ...tree, height };
      return tree;
    })
  );
}

// Somewhere else:
handleSetNewHeightForTree(0, 8);
```

### Sorting an Array of Objects

To sort an array of objects, you can use `sort` on a _copy of the array_ with a custom compare function. The compare function
returns a number, which is used to determine the order of the elements.

```js
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleSortTreesByHeight() {
  setTrees([...trees].sort((a, b) => a.height - b.height));
}
```

> 📙 Learn more about [**Updating objects inside Arrays** in the React Docs](https://react.dev/learn/updating-arrays-in-state#updating-objects-inside-arrays).

## Choosing the State Structure

There are some common pitfalls when choosing your state structure.

### Group Related State

If you have state that belongs (and updates) together, group it into a single object. This makes it easier to update the state.

```js
// ❌ MEH
const [userName, setUserName] = useState("Alex");
const [userAge, setUserAge] = useState(28);

// ✅ BETTER
const [user, setUser] = useState({ name: "Alex", age: 28 });
```

### Avoid Redundant State

If you have a value that is derived from a state, you should avoid storing it in state. Instead just use a normal variable.

The problem with redundant state is that it can get out of sync with the source of truth if you forget to update it correctly.

```js
// ❌ BAD
const [user, setUser] = useState({ name: "Alex", age: 28 });
const [isAdult, setIsAdult] = useState(user.age >= 18);

// ✅ GOOD
const [user, setUser] = useState({ name: "Alex", age: 28 });
const isAdult = user.age >= 18;
```

### Avoid Duplication in State

Avoid storing the same value in multiple places in state. This can lead to bugs and makes it harder to update the state.

```js
// ❌ BAD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [selectedTree, setSelectedTree] = useState(trees.find((tree) => tree.id === 0));

// Somewhere else:
setSelectedTree(trees.find((tree) => tree.id === 2));


// ✅ GOOD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [selectedTreeId, setSelectedTreeId] = useState(0);

const selectedTree = trees.find((tree) => tree.id === selectedTreeId);

// Somewhere else:
setSelectedTreeId(2);
```

### Avoid Having Duplicate Lists in State

If you have a list of items in state, you should avoid storing a derived version of it in a different state variable. This is a common mistake when you want to display a filtered version of the list.

```js
// ❌ BAD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [filteredTrees, setFilteredTrees] = useState(trees.filter((tree) => tree.height > 7));

// Somewhere else:
setFilteredTrees(trees.filter((tree) => tree.height > 9));

// ✅ GOOD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [minHeight, setMinHeight] = useState(7);

const filteredTrees = trees.filter((tree) => tree.height > minHeight);

// Somewhere else:
setMinHeight(9);
```

> 📙 Read more about [**Choosing the State Structure** in the React Docs](https://react.dev/learn/choosing-the-state-structure). The Docs have many more examples and explanations.

---

## Resources

- [Updating Objects in State (React Docs)](https://react.dev/learn/updating-objects-in-state)
- [Updating Arrays in State (React Docs)](https://react.dev/learn/updating-arrays-in-state)

