### Array Methods already known
* **map**     -> return new array and go through array
  * append `.map` to array and pass an anonymous function with an argument e.g. `myGames.map((game)=>{..., return game})`
  * the returned array needs to be saved in a variable, e.g. `const returnMap = myGames.map(...`
  * will return a boolean result (*true* / *false*), if an Object should be returned, needs an if-statement in the function body

* **filter**  -> filter array with given criteria and return a copy ("Shadow Copy Array")
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
returns the index number of the searched element

#### works only with the callback function
```js
names.findIndex((element) => element === "Maria"  // returns -1 if element is not found
// returns only the ~~first Element~~ and then stops
// also a case sensitive method
```
* **return notwendig**

## find
```js
names.find((element) => element === "Maria"  // returns undefined if element is not found
// returns only the ~~first Element~~ and then stops
// also a case sensitive method
```
* find has a callback with an index value -> record index value where the first item was found and continue from there (in a loop)
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find
* sollte find nicht in eine Zeile passen, braucht es ein **return statement**

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
* like .every and .include, .some returns a boolean 


<br>

<br>

-----------------------------------------------------------------------------------------------------------------------

<br>

# JS Array Methods 2

## Learning Objectives

- [ ] Understanding advanced array methods
  - [ ] `includes`
  - [ ] `find` and `findIndex`
  - [ ] `sort` and `reverse`
    - [ ] know how to use `slice()` to make a copy
  - [ ] `some` and `every`
  - [ ] `reduce`

---

## `includes`

Use `array.includes()` to check whether the array contains the specified value. If it does, `true`
is returned, otherwise `false`.

```js
const colors = ["hotpink", "aquamarine", "granite"];

colors.includes("aquamarine"); // true
colors.includes("nemo"); // false
```

---

## `find` and `findIndex`

Use `find()` to receive **the first element** of the array that satisfies the provided testing
function. Otherwise, it returns `undefined`.

```js
const colors = ["hotpink", "aquamarine", "granite", "grey"];

colors.find((color) => color.startsWith("g")); // 'granite'
colors.find((color) => color.startsWith("b")); // undefined
```

Use `findIndex()` to receive the index **of the first element** of the array that satisfies the
provided testing function. If there is no such element, `-1` is returned.

```js
const colors = ["hotpink", "aquamarine", "granite", "grey"];

colors.findIndex((color) => color.startsWith("g")); // 2
colors.findIndex((color) => color.startsWith("b")); // -1
```

---

## `sort` and `reverse`

Use `sort()` to sort the elements of an array. You need to provide a callback function in order to
tell how the array is sorted.

### Sorting Numbers

```js
const numbers = [4, 42, 23, 1];

numbers.sort((a, b) => a - b); // [1, 4, 23, 42]
numbers.sort((a, b) => b - a); // [42, 23, 4, 1]
```

The sorted order is based on the return value of `a - b` / `b - a` :

| Return value of `a - b` | sort order                         |
| ----------------------- | ---------------------------------- |
| > 0                     | sort `a` after `b`                 |
| < 0                     | sort `a` before `b`                |
| === 0                   | keep original order of `a` and `b` |

> 💡 `sort()` converts the elements into strings, then compares their sequences of UTF-16 Code units
> values. This is why `array.sort()` without a callback is mostly useless.

### Sorting Strings

In order to sort strings, you need to tell the `sort()` method two things inside of the callback
function:

- lowercase both strings before comparing them (uppercase works as well)
- using if-statements, be explicit about the return values dependent on the result of the comparison
  (`nameA < nameB` and `nameA > nameB`)

```js
const strings = ["Xbox", "PlayStation", "GameBoy"];

strings.sort((a, b) => {
  const nameA = a.toLowerCase();
  const nameB = b.toLowerCase();
  if (nameA < nameB) {
    return -1;
  }
  if (nameA > nameB) {
    return 1;
  }
  return 0;
});

console.log(strings); // ['GameBoy', 'PlayStation', 'Xbox']
```

> 💡 In UTF-16, the upper- and lowercase version of the same letter do not have the same value. An
> uppercase 'H' has the UTF-16 decimal value of 72, while the lowercase 'h' has a value of 104.
>
> For example, an uppercase 'W' (87) and a lowercase 'd' (100) are sorted behind the uppercase 'H'
> (72), but before the lowercase 'h' (104); the result would look like ['H', 'W', 'd', 'h']. This is
> why it's necessary to upper- or lowercase all letters before sorting them.

### `reverse`

In order to reverse an array, simply use `array.reverse()`. This can be combined with `sort()` as
well:

```js
const numbers = [4, 42, 23, 1];

const reversedNumbers = numbers.reverse(); // [1, 23, 42, 4]
```

### `slice`

It's important to note that some array methods, as `sort()`, do not create a new array, but mutate
the original one.

```js
const numbers = [4, 42, 23, 1];

console.log(numbers); // [4, 42, 23, 1]

const sortedNumbers = numbers.sort((a, b) => a - b);

console.log(sortedNumbers); // [1, 4, 23, 42]
console.log(numbers); // [1, 4, 23, 42]

// What happens if sortedNumbers is reversed?

const reversedSortedNumbers = sortedNumbers.reverse();

console.log(reversedSortedNumbers); // [42, 23, 4, 1]
console.log(sortedNumbers); // [42, 23, 4, 1]
console.log(numbers); // [42, 23, 4, 1]
```

This behaviour will often cause errors. To prevent it, just make a copy of the original array using
`slice()`.

```js
const numbers = [4, 42, 23, 1];

console.log(numbers); // [4, 42, 23, 1]

const sortedNumbers = numbers.slice().sort((a, b) => a - b);

console.log(sortedNumbers); // [1, 4, 23, 42]
console.log(numbers); // [4, 42, 23, 1]
```

---

## `some` and `every`

Use `some()` to test whether **at least one element** in the array passes the provided test.

```js
const colors = ["hotpink", "aquamarine", "granite"];

colors.some((color) => color.startsWith("g")); // true
colors.some((color) => color.startsWith("i")); // false
```

In order to check if **all elements** pass the test, use `every()`.

```js
const colors = ["hotpink", "aquamarine", "granite"];

colors.every((color) => color.length > 5); // true
colors.every((color) => color.length < 3); // false
```

---

## `reduce`

`Array.reduce()` is an array method to reduce a list of values into a single value.

It has the following core features:

- starting from the beginning, it executes the callback function on each element of the array,
- the return value of each calculation is passed to the next calculation (i.e. it becomes the new
  starting value for the next iteration through the array)
- the final result is a single value.

It's main use case is to calculate the sum of an array of numbers.

```js
const numbers = [4, 42, 23, 1];

numbers.reduce((a, b) => a + b);

console.log(numbers); // 70
```

> ❗️ If you find yourself doing anything more complex than this with reduce (like reducing an array
> to an object, etc.) you should try to find another solution to your problem. Complex reduce
> functions are very hard to read and thus error prone.
>
> Example of reducing an array to an object without `reduce()`:
>
> ```js
> const myArray = [
>   { foo: 1, bar: "hi" },
>   { foo: 4, bar: "hey" },
>   { foo: 2, bar: "ho" },
> ];
> const myObject = {};
> myArray.forEach((element) => {
>   myObject[element.bar] = element.foo;
> });
>
> console.log(myObject); // {hi: 1, hey: 4, ho: 2}
> ```

---

## Resources

- [Searching Arrays (javascript.info)](https://javascript.info/array-methods#searching-in-array)
- [sort (javascript.info)](https://javascript.info/array-methods#sort-fn)
- [reduce (javascript.info)](https://javascript.info/array-methods#reduce-reduceright)


