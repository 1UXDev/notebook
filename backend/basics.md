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

<br>

### Beispiele

**Beispiel: Produkte anzeigen**

_REST Struktur_
* GET /products zeigt alles
* GET /products/:id zeigt ein spezifisches Produkt
* POST /products -> add a new product to the database

*Alternative zu REST wäre GraphQL*

<br>

**Beispiel Express**
```jsx
import express from "express"
const persons=["yair", "klaus", "gimena"]
const app = express()

app.gt("/",(req, res)=>{
 response.json({text: "Hello from the server"})
})
```
In another directory "Client"

**Other Notes**
* Cors - Cross Origin resource sharing; also a npm package as Middleware 
* Postman & isomnia -> Tools for http requests
* Applications in React need to be **build** `npm run build``
  * puts all code in one line, removes spaces where not needed

<br>

------------------

<br>

[From](https://github.com/spiced-academy/chicory-web-dev/tree/main/sessions/build-a-server)

## Node
* node is a runtime environment for js, to make it executable outside of the browser
  * can be used for more than a server
  * With node functionalities we do not need to install them, but import them
 
```jsx
// use the node internal module fs-filesystems (data.json is in a different folder and holds an array with objects)
import fs from fs

// --- read file ---
const fileData = fs.readFileSync('./data.json')
// the "sync" can also be left out, but readFile then needs to call the write when its ready, otherwise it may try to write before its done processing / loading

// -- we ned to change the data to a js object --
const jsonData = JSON.parse(fileData)

// --- modify that array ---
jsonData[0].name = "Johanna Leon"

// --- write to file ---
fs.writeFileSync("./data.json", JSON.stringify(jsonData))
```
* you could also create new directory, delete files, get all names of images, etc.


<br>

<br>

------------------

<br>

## Minimal server

Installation
```bash
$ npm install express cors
```

Running the server
```bash
$ node server.js
```

When you are too tired of stopping / restarting the server
```bash
$ npm install -g nodemon
$ nodemon server.js
```

Communicating with that server from a React app
```
fetch('http://localhost:8000)
```

<br>

<br>

-----------------------

<br>

```jsx
// Server.js
import express from 'express'
 
import cors from 'cors'


const persons = ['yair', 'klaus', 'gimena']

const app = express()

// this is to solve the CORS problem of the browser
app.use(cors())

// routes
app.get('/', (request, response) => {
	response.json(persons)
})

// https://github.com/<username>

app.get('/about', (req, res) => {
	res.json({text: 'hello from about'})
})
/*
GET /products -> all products
GET /products/:id -> one product
POST /products -> add a new product to the database
*/
app.get('/:user', (req, res) => {
	// access the route parameter
	// req.params.user
	res.json(req.params)
})


app.listen(8000, () => console.log('Server listening on port 8000'))
```

-----------------

```jsx
// Storage.js

// we use the node internal module fs - filesystem
import fs from 'fs'

// reading from a file
const fileData = fs.readFileSync('./data.json')
// we need to change the data to a js object
const jsonData = JSON.parse(fileData)
console.log(jsonData)

// modify that array
jsonData[0].name = "John Lennon"

// write to a file - we need to turn the js object to a string
console.log(jsonData)
fs.writeFileSync('./data.json', JSON.stringify(jsonData))


```
