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
** When we are ready, we will call your function**

