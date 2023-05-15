# Nesting
**putting elements into each other, e.g. arrays within arrays that i loop through**
* check the package.json: "main" is the "start" of the project (usually src/index.js)
* what dependencies are required?
* Props is an object holding the properties and passing Information to react components
* JSX Fragments (empty <> </>) can be used to wrap components without adding additional DOM-Elements

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
      <h1> Animal Shelter</h1>      // define prop-contents
      <Animal emoji=🐕 name="Lucky" description="A good dog"/>     
      <Animal emoji=😺 name="Sheeba" description={"A nice cat".toUpperCase()} />  // strings can be used in curly brackets but only makes sense if you also want to use JS 
      <Animal emoji=🐢 name="Gaia" description={<strong>"Ninja Turtle"</strong>} />   // you could also use JSX 
      <Animal emoji=🐔 name="Chicky" description={
        <ul>
          <li> Chirpy </li>
          <li> Cheerful </li>
        <ul>
      } />
   </main>
   )
}

function Animal({emoji, name}){   //receive props (that are destructured)
  return (
  <>
    <h2> 
      {emoji} {name}      // render props in Component    
    </h2>
    <p> {description} </p>
   <Button name={name}></Button>     // passing "name", that was defined in main and handed to "Animal" to the button component   
   </>
  )
}

   // Better way to do that is with {children}
   // replace the prop in "Button"-Component with {children} and:
        // <button type="button" className="button">
            //   {children}
        // </button>
   // now, in the App-Component the Button can be used with other values in a slightly different Syntax:
        // <Button>Adopt {name}!</Button>
        // or
        // <Button> Login </Button>
   // it allows composing one component out of others and makes it more versatile
        
        
        
const Button = ({name}) =>{
  return (
    <button type="button" className="button">
      Adopt Me!
    </button>
  )
}
```

## Children Tag






