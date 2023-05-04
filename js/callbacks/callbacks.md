## Callbacks
**e.g. addEventListener: User triggers Event**

* has to be called with an argument (e.g. the event to preventDefault)

#### Callback functions we know already
```javascript
const button = document.querySelector("button");
const form = document.querySelector("form");

button.addEventListener("click", function(){
  console.log("button clicked")
}

form.addEventlistener("submit", (e) =>{
  e.preventDefault();
  ...
}
```

#### Callbacks in functions - Examples
```javascript

// Anonymous functions
saveButton.addEventListener("click", function(){    //arrowfunction would also be possible
  ...
}

// named functions
function handleCancel(){
  ...
}

//Combining both
cancelButton.addEventListener("click", handleCancel){   // no parenthesis after handleCancel, because we don't want to call it, just pass it as Argument
  ...
}

// Receiving Argument in the callback
restoreButton.addEventlistener("click", (event)=>{
  console.log
}

const mouseTrap = (mouse) =>{    // function with the argument mouse
  console.log(mouse.name)       // mouse.name looks back to where it was called and uses that as the event
}

skipButton.addEventListener("click", mouseTrap); // a function that is called with a string and the function argument passed as "mousetrap"

```
<br>

#### Higher Order functions

```javascript
function upperCase(text){   // logs text in Uppercase
  const upper = text.toUpperCase();
  console.log(upper);
}

upperCase("hi there")   // Output: HI THERE

// higher Order function
function showText(transformation){   // When you're ready, trigger the eventLlistener [transformation is a name for the "mouseTrap"
  transformation("Changed by the Callback Function");
}

showText(upperCase)   // passing the upperCase function along
```

1. call showText-function with upperCase as argument
2. showText has "transformation" as Parameter, which will be "upperCase"
3. showText function body is executed, which means "upperCase" is triggered as function, that has the argument ("Changed by the Callback Function")
4. the upperCase function is then executed, the parameter "text" is filled with the string, transformed to upperCase and logged

*e.g. useful for asynchronus scenarios, where some task is not finished right now, but will be in the future and we want it to do something later*

**When we are ready, we will call your function**


<br>

[](https://github.com/mntzd/notebook/blob/main/js/callbacks/callback.png)
![Example of a callback](https://github.com/mntzd/notebook/blob/main/js/callbacks/callback.png "Example of a Callback")

<br>

-------------------------------------------

<br>

# JS Callback Functions

## Learning Objectives

- Understanding the concept of callback functions
- Using an anonymous callback function
- Using a named function as a callback function
- Knowing what a higher order function is

---

## Callback Functions

A callback function is a function that is passed **as an argument** into another function.

The outer function can execute this callback function at the correct moment or multiple times, for
example:

- when an event is triggered
- when the fetched data arrived on your computer
- for each element in an array.

Callback functions are used, whenever the program itself needs to figure out **when** or **how many
times** the function needs to be executed. We already used callback functions in **event
listeners**:

```js
button.addEventListener("click", () => {
  console.log("Inside the callback function.");
});
```

Here the structure is as follows:

- outer function: `addEventListener()`
- first argument: `'click'`
- second argument: callback function
  ```js
  () => {
    console.log("Inside the callback function.");
  };
  ```

This type of function is called **anonymous function**, since it is declared without giving it a
name.

## Named Callback Functions

Any function can be used as a callback function. It just needs to be passed to another function. You
can declare a normal function and then use the **name of the function** to pass it into another
function:

```js
function sayHello() {
  console.log("Hey Dude!");
}

button.addEventListener("click", sayHello);
```

> ❗️ Note that we do not call the function here (we wrote `sayHello` instead of `sayHello()`). We
> only pass the function to the event listener. The function is only called when the event happens.

## Higher Order Functions

A higher order function is a function that takes a **callback function as an argument** and **calls
the callback function** inside their body, e.g. the `addEventListener` method.

```js
// this function calls its callback function 3 times!
function myHigherOrderFunction(callback) {
  callback();
  callback();
  callback();
}
```

We will encounter these higher order functions in future sessions:

- `.then`
- `.forEach`
- `.map`
- `.filter`

> 💡 Don't worry, you don't have to write higher order functions yourself, you only apply them to
> solve certain problems.

## Parameters in Callback Functions

A callback function can accept parameters. The values for the parameters are provided by the
function, that calls the callback function (the "higher order function").

In this example the callback function can accept a parameter to retrieve information about the
occurred event:

```js
button.addEventListener("click", (event) => {
  console.log("This button was clicked:", event.target);
});
```

---

## Resources

- [MDN Callback Functions](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)
