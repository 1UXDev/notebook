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

#### Anonymous functions
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
