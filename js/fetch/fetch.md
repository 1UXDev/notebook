```js
import { CardsDisplay } from "../components/CardsDisplay/CardsDisplay.js";
import { Button } from "../components/CardsDisplay/Button.js";

const main = document.querySelector("main");
const playButton = Button("Play");
const resetButton = Button("Reset");
const cardsDisplay = CardsDisplay();

main.append(playButton, resetButton);
main.prepend(cardsDisplay); // prepend, so it comes first in DOM

playButton.addEventListener("click", asynch () => {     // define function as asynchronous
  // console.log("Listener is Working")

  try {
    const response = await fetch("https://urltomyAPI.com/api/...");      // await keyword

    const cards = await response.json()       // every function that works with promises returns a promise, thus it needs an await keyword
                                                // you get a response but not yet the data, that what the .json() is for
    let cardSet ="";
    cards.cards.forEach((card) => {
        cardSet += `<img src="${card.image}"/>`
    })       // access cards-Array in cards-Object

    cardsDisplay.innerHTML = cardSet;
    }

    catch(error){
        console.log(error)
    }
});
```

When exported:

```js
// getCards.js
export const getCards = async (numOfCards = 2) => {
  try {
    const response = await fetch("https://urltomyAPI.com/api/...");
    let cardSet = "";

    if (!response.ok) {
      console.error("bad response:", response.status);
      cardSet = "Oops! Try again";
      return cardSet; //return statement triggering if response is not ok
    }

    const deck = await response.json();

    deck.cards.forEach((card) => {
      cardSet += `<img src="${card.image}"/>`;
    });

    cardsDisplay.innerHTML = cardSet;
    return cardSet;
  } catch (error) {
    console.log(error);
  }
};
```

---

## Notes

### when importing asynch functions you have to also "await"

```js
playButton.addEventListener("click", asynch ()=>{
    let myVar = await getCards()
})
```

### you can use literals with URLs

```js
const response = await fetch(`https://urltomyAPI.com/api/${myVar}`);
```
