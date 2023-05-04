# forEach
```javascript
array1.forEach(function(el) {   // function does not need name since its only called here
  console.log("hello")
})
```

```javascript
// Having an Array with Objects (Games) in it

games.forEach(game => console.log(game.name.toUpperCase)
//note: you cannot "return" forEach, it goes through the whole thing
```
*like a for-of loop, but does a callback for each Element (?)

# Map
*Change every Element of the Array (but length of array has to stay the same)*

```javascript
const names = games.map((game) =>{    // goes through all elements of Array and does something with them, puts the result in the place of the old Arrayitem but in a new Array
  return game.name      // returns values of name-keys for each game-Object in the array
})

console.log(names)

------------------------------------

const names = games.map((game, i) =>{   // second optional paramter for index [could also include 3rd parameter for the array itself] -> refer to mdn documentation 
  ...
})
```

### custom Maps / Understanding the map function
-> Whats going on inside the map function?
```javascript
function myMap(arr, myCallback){    // myMap(arr, callback
  const res = [];
  for (let el of arr){              // iterate over passed / called array and puts it into "res"
    const name = myCallback(el)     // get the name through myCallback (= myM
    res.push(el)            
  }
  return res
}

const result = myMap(games, (game) => {   // this function returns the name of a passed object
  return game.name                        // this could also return other values, e.g. return "game.name[0]" 
}

console.log(result)
```

<br>

## filter

*creates new array with items that match a provided condition*

```js
const filtered = games.filter(game =>{      // executed as many times as item in array
  if (game.publishingYear < 2000){          // define when to return true and when false
    return true
    } else { return false}
});

console.log(filtered);                    // returns an array with all games released before 2000
```

