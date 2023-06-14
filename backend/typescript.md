# Typescript
adds types to javascript -> prevents errors like `undefined`

**The general process**
1. Install Typscript & set up Typescript environment
2. write your code in .ts files
3. code is interpreted (with React in the Background): the generated js file looks normal, but the resulting js can now only use the "legal" ways we defined in the typescript file
4. run via `tsc index.ts` to see output in console
5. Result: Single JS-file where everyhting is inside

<br>

**ts init**
creates tsconfig.json to configure what kind of JS-Flavor to create

*Possibly interesting settings in the tsconfig:*
* noEmitOnError by Default set to true (Does not emit JS file when error happens)
* TSC with Watch Option --> will constantly monitor typscript file (when changed, js will be updated)

<br>

<br>

## Types in Typescript
supports Number, String, Boolean, null, undefined, infinity, minus infinity
* if you do not assign a type, it will be `any`, which defeats the purpose of typescript

```jsx
let n: string = ""
// n = 123 // will not work since it is not the declared type
// always useful to initialize a variable with a placeholder of the type (e.g. an empty string, false, ...)
```

<br>

<br>

------------------

<br>

## Arrays, Objects and other Snowflakes
### Arrays
Arrays in js can stroe mixed values `["Number of Apples", 3, true]` 
-> but this is considered bad practice in lots of programming languages 

```jsx
let arr : number[] = [1,2,3]
arr.push(true)          // will not work cause boolean is not a number
const num = arr.pop()   // with typescript we can be sure that the result is either a number or undefined

if (num){
  console.log(num)      // console.log will always log a number (if it logs), since the condition is either a number or false
}                       // edge case if num is 0, the "if" will not be executed, because it is falsy

function add(a: number, b: number): number{   // define the arguments as type:number AND the type of the return value
  return a + b                                // if you forget to add a "return", typescript will also give an error
}

const result = add(1,4)
```

<br>

### Union-Types
Defining one variable as 2 possible types
-> Special typescript syntax for this, using a pipe > | < symbol

```jsx
  let username: undefined | string = undefined    // while we do not yet have a username it is undefined, when we do, it will be a string
  
  const m: undefined | string = Math.random() > .5? undefined : "hello"
  console.log(m.length)                           // returns an error, because it may be undefined
  console.log(m?.length)                          // returns then length if it's a string, otherwise it is undefined
  // also more complex conditions could be rendered here
```

**can also be used with different values 4|5**
```jsx
let salut: "hi" | "hello"
// salut = "hi"     // -> Hovering over it gives us tooltip with possibly assignable values
// This would only accept "hi" or "hello" as values - or throw an error

// Example:
let salutation: "hi" | "hello" = Math.random() > .5? "hi" : "hello"   // randomly selects hi or hello

if(salut != hello){
  console.log(salut)      // has to be "hi" since it cannot be "hello"
}
```

<br>

### Objects

```jsx
let user{
  id:number,
  email?:string,    // the "?" marks email as optional, that means it could be string or undefined
  name:string
} = {
  id: 123,
  // email: "",
  name: "",
}

console.log(user.email.length)    // returns undefined, since the length attribute cannot be read from something that is undefined
// ... so we would have to make sure it is not undefined :)

```

**Annotating variables - use with caution**
```jsx
// lets assume we get "user" from an external source
const email = user.email as string        // we annotate email as string

console.log(email.length)     // ultimately it can still crash, if the value was undefined
```


#### Type Alias
-> works as replacement of types

**directly assigning type-alias**
```jsx
type TypeA = string

function returnInput(str: TypeA):string {
  return str
}
```

**Using & Combining Type Alias
```jsx
type User = {
  id:number,
  email?:string,
  name:string
} 


// imply that the userArray might be empty on purpose 
let loggedInUser: User | null = null;  


// - ! - combine type aliases
type Admin = {
  adminPassword: string,
} & User        


let user : User = {
  id: 123,
  // email: "",
  name: "",
}

let admin: Admin = {
  id:123,
  name: "sven",
  adminPassword: "$3cr3t!
}

admin.
```

#### Interfaces
Similar to alias.
* but you can declare two interfaces and it does not give an error
* Don't do this

```jsx
interface User = {
  id:number,
  email?:string,
  name:string
} 

interface Admin extends User = {
  adminPassword: string,
}

interface Admin = {               // you can "extend" the Admin with Admin and add to it
  adminPreference: "Darkmode",    // but this can easily get confusing
}
```

<br>

<br>

------------------

<br>

## Type Parameters
* 🚫 Too complicated arr: string[] | number [] | ...
* 🚫 Looses the Type in the further process: arr: any[] 
* ✔️ Create a variable holding the Types

```jsx
let arrofNumbers: Array<number>

function getLastElement<T>(arr: T[]):T | undefined {        // Alternative Syntax: function getLastElement<T>(arr: Array<T>):T{
  return arr.pop()
}

let lastElement = getLastElement([1, true])
lastElement = 12

lastElement = ""      // will throw an error, because String was not allowed in the definition
```

<br>

----------------------------


### Further Reading
- Django / possibly also Flask
- How to creat your own server
- Var and js/React Classes
