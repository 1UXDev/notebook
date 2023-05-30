# Global State
* We need information inside a child component
  * instead of lifting up, handing down etc. pp we simply **put all states** into the App component on the very top (or highest shared parent)
  * we need to pass down the prop to the children of the children if they need it -> **drilling**
  * Naming is very important, otherwise you later-on do not know what is what
* We look at every Component and move the functionality and renders and put everything back into the App??

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
  
  return(
  <Layout>
    <Component {...pageProps} animals={animals} handleAdd={/> // Passing it down to the X components that need those props
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


## Redux
* Redux creates a place to save variables and work with them
* Complicated to set up but then you don't have to 

## Zustand
* like redux, but a lot easyer to set up
