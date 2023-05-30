# Global State
* We need information inside a child component
  * instead of lifting up, handing down etc. pp we simply **put all states** into the App component on the very top (or highest shared parent)
  * we need to pass down the prop to the children of the children if they need it -> **drilling**
  * Naming is very important, otherwise you later-on do not know what is what
* We look at every Component and move some variables and function and move things up into the App :(
* We try to create a single source of truth with moving everything up



**Example**
```jsx
// ---- in App.js
// -- intialize Array
const initialAnimals = [         
  {id: 1, name:"Cats", count:0},
  {id: 2, name:"Dogs", count:0},
  {id: 3, name:"Mouses", count:0},
]

export default function App({Component, pageProps }){
  const [animals, setAnimals] = useState(initialAnimals) // Define the animals-Array as Variable
  
  function handleAdd(animalID){
   setAnimals(animals.map(animal) => animal.id === animalId ? {...animal, count: animal.count+1} : animal)
   // everytime i press the +button: loop through animals, if the id is same as the one i pressed, spread array and add +1 to the animal value; otherwise do nothing
  }
  
  const dragonsCount = animals.find((animal)=> animal.name === "Dragons").count;
  
  const AnimalsCount = ()=>{
   let count = 0
   animals.forEach((animal=>{
     count += animal.count
    })
  }
  
  return(
  <Layout dragonsCount={dragonsCount}>
    <Component {...pageProps} animals={animals} handleAdd={handleAdd}/> // Passing it down to the X components that need those props
  </Layout>
  )
}

// -------------------------------------------------------------------

// ---- in child.js
// ... 
return(
  <List>
    {animals.map((animal)=>{
        <Counter animalName={animal.name} />
      }
    )}
  </List>
// ...
)


```


## Helpful Frameworks
**Redux**
* Redux creates a place to save variables and work with them
* Complicated to set up but then you don't have to 

**Zustand**
* like redux, but a lot easyer to set up
* Saves all the variables and functions in a folder called "stores" with a .js file
* bot h frameworks are faster, becuase they do not re-render the whole App but only the part that we need to re-render
