* DOM Tree is updated
* Better to use form element for A11y instead of just creating a input + button that is listened to
* `const newElem = document.createElement("h1")`
* * newElem.classList.add("card") // how to add a class
* * you could add Text to an Element like this: `newElem.textContent = "some Text here"`
* * Alternative: newElem.innerHTML = "<h1>my headline text</h1>" //possible security risk though
* const cardText = textInput.value
```javascript
myElem.innerHTML = `
<h2> Card </h2>
<p> ${cardText} </p>
console.log(myElem)
`
```

**-->** `cardContainer.append(myElem) // append created DOM-Element to HTML`
* `text.input.value = "" // reset the value of the input field` 


___________________
note: the append-method needs a DOM-Element, thats why you create it with js first and not simply say .append("<h1>...</h1>")
