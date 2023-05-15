# Nesting
**putting elements into each other, e.g. arrays within arrays that i loop through**
* check the package.json: "main" is the "start" of the project (usually src/index.js)
* what dependencies are required?
* Props is an object holding the properties and passing Information to react components

```jsx
root.rende(
  <StrictMode>
    <App />
  </StrictMode>
```

```jsx

```

## Props
define, receive, render


```jsx
export default function App(){
  return (
    <main>
      <h1> Animal Shelter</h1>
      <Animal emoji=🐕 name="Lucky"> />     // define prop-contents
      <Animal emoji=😺 name="Sheeba"> />
}

function Animal({emoji, name}){   //receive props (that are destructured)
  return (
    <h2> 
      {emoji} {name}      // render props in Component
    </h2>
  )
}
```
