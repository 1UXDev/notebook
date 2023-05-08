### Array Methods already known
* **map**     -> return new array and go through array
  * append `.map` to array and pass an anonymous function with an argument e.g. `myGames.map((game)=>{..., return game})`
  * the returned array needs to be saved in a variable, e.g. `const returnMap = myGames.map(...`
  * will return a boolean result (*true* / *false*), if an Object should be returned, needs an if-statement in the function body

* **filter**  -> filter array with given criteria and return a copy ("shadowarray")
  * ```const returnFilter = myGames.filter((item)=> item.publishingYear > 1989);```
  * returns the Objects for the condition
* **forEach** -> loop the array one time, does not return anything (so no return statement)

<br>

# Find Things in Arrays
## Includes
* checks if a given value is present - only used for arrays (not for objects) - returns true or false
```js
const names = ["Maria", "Gimena", "Inciarte"];

const returnIncludes = names.includes("Maria")  // returns true
// note: the method is case-sensitive, so always put in .toUpperCase() or .toLowerCase()

// Multiple possibilities for Uppercasing: forEach Loop or .map
names.forEach((element, index)=>{     // index is optional, but good to replace values in array
  element.toLowerCase().includes("maria");
  // no you'd have to save the result somewhere, you could push it to the original array in the corresponding place
})
```

## findIndex
`let myName = names.findIndex("Maria")` **-> Does not work, the findIndex needs a callback function**
#### works only with the callback function
```js
names.findIndex((element) => element === "Maria"  // returns -1 if element is not found
// returns only the ~~first Element~~ and then stops
// also a case sensitive method
```

## find
```js
names.find((element) => element === "Maria"  // returns undefined if element is not found
// returns only the ~~first Element~~ and then stops
// also a case sensitive method
```
* find has a callback with an index value -> record index value where the first item was found and continue from there (in a loop)
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find

<br>

# Sorting Arrays
* JS converts arrayvalues into strings and compares their UTF-16 values
* ASCII Table 128 Symbold that can be represented (only English); Unicode is an extension of ASCII (e.g. Greek or Umlaute)
* Sort Ascending is not "1,2,10,..." but "1,10,2..."

## .sort
```js
const sortedByAge = students.sort(a,b) => a.age - b.age
const sortedByName = students.sort((a,b) =>{
  const nameA = a.name.toLowerCase();           // bring everything into same case
  const nameB = b.name.toLowerCase();           // otherwise Uppercase comes before Lowercase in sorting 
  if (nameA < nameB){                           // the sorting works with 1, 0, -1 so we have to return these values in a loop
    return -1;                                  // if you change around the 1 & -1  values, the ordering is reversed
  } else if (nameA > nameB){
    return 1;
  }
  return 0
}
```
**Sort uses the original array and alters it, so the original array is always like the most recent sort request**
* thus when doing multiple sorts, we have to save the newly sorted array
`const sortedByAgeCopy = students.slice().sort(...)  // slice without Arguments just creates a copy in the variable` 

## .some
```js
students.some((student)=> student.points === 0)
} // returns true once it has found something
```



