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

```bash
touch {avatar, logo}.js
```

## Props
define, receive, render

## Children
* is a reserved keyword in react!!

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
<br>

<br>

------------------------------------------------

<br>


# React Nesting

## Learning Objectives

- Understanding the concept of nesting
- Creating multiple custom components to create a hierarchy
- Using the `children` prop to render JSX from the parent component
- Understanding composition as a way to build complex components

---

## Passing JSX as Props

Elements created by JSX are just objects. They can be passed around like any other object: for example, as props.

```js
function UserCard({ avatar }) {
  return <div className="card">{avatar}</div>;
}
```

```js
function App() {
  return <UserCard avatar={<Avatar />} />;
}
```

## The `children` Prop

You are already familiar with nesting built-in browser tags:

```js
<div>
  <img />
</div>
```

Oftentimes you'd want your own components to be nestable as well.

```js
<UserCard>
  <Avatar />
</UserCard>
```

If you nest a component inside of another component, the nested component is passed as a prop to the parent component. This special prop is called `children`.

```jsx
function UserCard({ children }) {
  return <div className="card">{children}</div>;
}
```

This component will render the nested element(s) as a child of the `div` element.

> 💡 The nested element(s) can be a single element, multiple elements, or even a string or number.

> 📙 Read more about [**Passing JSX as children**
> in the React Docs](https://react.dev/learn/passing-props-to-a-component#passing-jsx-as-children).

## Fragments

Sometimes you want to return multiple elements from a component function without wrapping them in a `div` or other element. You can use a `Fragment` (`<></>` or `<Fragment></Fragment>`) for this.

This is necessary because React components can only return a single element from a component function.

```jsx
function UserList() {
  return (
    <>
      <UserCard>
        <Avatar />
      </UserCard>
      <UserCard>
        <Avatar />
      </UserCard>
    </>
  );
}
```

This is equivalent to the following, but the shorthand version above is generally preferred.

```jsx
import { Fragment } from "react";

function UserList() {
  return (
    <Fragment>
      <UserCard>
        <Avatar />
      </UserCard>
      <UserCard>
        <Avatar />
      </UserCard>
    </Fragment>
  );
}
```

> 💡 The `<Fragment></Fragment>` syntax is only necessary if you want to pass the special `key` prop to the fragment, which will become important when you start working with lists.

> 💡 When researching you sometimes might see `<React.Fragment></React.Fragment>`, which is the same thing.

> 📙 Read more about [**Fragment (<>...</>)**
> in the React Docs](https://react.dev/apis/react/Fragment).

---

## Composition

When we build React applications, we often want to build complex components from simpler components. This is called composition.

To do so you need to break down you application into components. You can then compose these components to build more complex components.

It is important to figure out which components you need and how they should be composed. This is called application design.

> 📙 Read [**Thinking in React**
> in the React Docs](https://react.dev/learn/thinking-in-react) up to and including Step 2. Later steps require state, which we will cover in a future session.

---

## Resources

- [Passing JSX as children in the React Docs](https://react.dev/learn/passing-props-to-a-component#passing-jsx-as-children)
- [Fragment (<>...</>) in the React Docs](https://react.dev/apis/react/Fragment)
- [Thinking in React in the React Docs](https://react.dev/learn/thinking-in-react)

