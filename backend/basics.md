* Applications in React need to be **build** `npm run build``
  * puts all code in one line, removes spaces where not needed

## Express
* Express.js: web framework for node.js
* 2 ways to use express, either with require or via import (which can only run in a module). It makes sense to have the same logic in front and backend, thus we use import with 2 possibilities:
  * 🚫 The worse approach: rename file to index.mjs
  * 🙌 Better Approach: package.json, change "type" to module

```jsx
import express from 'express'

const app = express();

// --- Define Routes of Server ---
// -- Which http requests are we accepting? e.g. GET POST PUT DELETE --

// - adding a GET-Route - 
app.get('/', ()=>{
  console.log("get home page")
}) // but this does not do a request, since it runs on the server, but it ––accepts–– it

// Script listens to incoming http requests
app.listen(8000, ()=>console.log('Server listening on port 8000')

// When we know send a get-Request (e.g. by going to localhost:8000) we will log "Server listening on ..." in the console

// --- Return something on the request ---
// -- enhance the get-route written before and replace it with this: --
app.get("/", (request, response) => {
  response.sendFile()
})
// Could also directly render HTML

app.get("/about", (req, res)=>{
 res.json({})
})

// paths as variables with ":"
app.get("/:username/:repo", (req, res)=>{
 //access the route parameter
 res.json(req.params)
})
// if user types localhost:8000/yair/23 it returns username: yair, repo:23

```
* Reihenfolg ist hier wichtig, die erste Route die passt wird genommen, deshalb müssen nicht-variablen-namen weiter nach oben

### Produkte anzeigen

**REST Struktur**
GET /products zeigt alles
GET /products/:id zeigt ein spezifisches Produkt
POST /products -> add a new product to the database

*Alternative zu REST wäre GraphQL*

```jsx

```
