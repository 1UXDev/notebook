# loops

## while loop
**-> e.g. to log something excatly x-times**
```javascript
let str ="a"
while (str.length<=8){  // Condition: while true -> do X
  console.log(str)
  str = str + str;     // necessary, so condition is not infinitely true
  // expected CL: "a" "aa" ... "aaaaaaa"
}
```
<br>

## for loop
**-> e.g. to log something x-times**
```javascript
for (let i=0;i<5; i++){   // initialize variable; if i is smaller than 5 -> execute, increment
  console.log("hello");   // increment could also be i = i + 3 [or a variable / function]??
}
```
* technically it would also be correct to initialize a string, define string length as stop-condition (researchmore here, not yet fully understood), also possible with functions / arrays / Objects??
* a **return** statement in a loop that is **inside a function** would **end the loop**
<br>

### for of loop
**-> e.g. to loop over array**
```javascript
let arrayName = ["abc", "zdf", "ard"]
for (variableName of arrayName){    // Naming convention: for (button of buttons){...}
  console.log(variableName)         // Output: abc, zdf ,...
  console.log(variableName[0])      // Output: a, z, ...
}
```
<br>

### for in loop
**-> used for objects**
* same syntax as for of, but is counting indexes
```javascript
let arrayName = ["abc", "zdf", "ard"]
for (variableName in arrayName){    // Naming convention: for (button in buttons){...}
  console.log(variableName)         // Output: 1, 2 , 3 [the indexes of the items in the array]
  console.log(arrayName[variableName])      // Output: abc, zdf, ard
  }
```
<br>

#### for in loop with objects
```javascript
const person = {
  name: "alex",
  age: 26,
  email: "alex@gmail.com",
}

for (let x in person){
console.log(person[x])    // you cannot use dot-notation here, because x is a variable and the interpreter does not know that it is supposed to be e.g. ".name"
}                         // expected output: alex, 26, alex@gmail.com
```


