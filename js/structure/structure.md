# Optimizinh JS Structure
* folder: utils -> contains e.g. authors.js
* "export" works with functions, variables, arrays, objects 
* "import" needs an importtype (like "data") and imports them as object

```js
//exporting stuff
export default

// importing stuff
import {data} from "./utils/authors.js"
// > when i export multiple things in one file, I need to explicitly define the "data" into {dataname}
import {authors} from "../../beispielOrdner.js"
// > importing multiple exports from a single file
import {xyz, def, poiuzt} from "../../beispielOrdner.js"


// Wrapping the contents to be exported into a function
export function MyFunctToExport(){     // Function that is a Component starts with a capital letter 
  let myVar = something.something
  ...
  return myVar
} 
```

```
// in the other file:
const header = Header()     // needs to be called since its a function
```

### making imports/exports reusable
```js
function Card(props){
 // stuff happening here
 let myVar = props.length
 
 return card
}

authors.forEach(author)=>{
  const cardElement = Card(author);
  body.append(cardElement)
}
```
