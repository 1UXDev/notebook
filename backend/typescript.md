# Typescript
adds types to javascript -> prevents errors like `undefined`

**The general process**
1. Install Typscript & set up Typescript environment
2. write code in .ts files
3. code is interpreted (with React in the Background)
4. run via `tsc index.ts`
5. Result: Single JS-file where everyhting is inside

### ts init
creates tsconfig.json to configure what kind of JS-Flavor to create
**Possibly interesting settings**
* noEmitOnError by Default set to true (Does not emit JS file when error happens)
* TSC with Watch Option --> will constantly monitor typscript file (when changed, js will be updated)

<br>

<br>

## Types in Typescript
supports Number, String, Boolean, null, undefined, infinity, minus infinity
* if you do not assign a type, it will be `any`, which defeats the purpose of typescript

```jsx
let n: string
// n = 123 // will not work since it is not the declared type
// always useful to initialize a variable with a placeholder of the type (e.g. an empty string, false, ...)
n= " "
```

<br>

### Arrays and Objects
#### Arrays
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

<br>

----------------------------


### Further Reading
- Django / possibly also Flask
- How to creat your own server
