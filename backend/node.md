# Servers
* browser and Node have a large intersection but:
  * Browser: DOM, alert, document, ... 
  * Node: files, OS processes, Serving / listening

If time, look at: 
* deno
* ports (wikipedia, which port is for what)

## Build a server with Node
```jsx
//--- server.js using node API

import { createServer } from `node:http`

const server = createServer((request, response)=>{   // Callback will be called everytime with the listen
    console.log("I got a request")  // this code does not go to client, it runs on server and sends response as http-response to client
    
    if(request.url === `/secret`){
      response.statusCode = 200;
      response.end("Not telling you")
    }
    
    // "response" tells node how to respond
    response.statusCode = 404;    // gives response a status-code of 200
    response.end("Not found")     // sends this content 
  });
  
  export {server};                // could also use React-like syntax export default const server = [...]
  
// --- in index.js ---
// Splitting Server into 2 files to 
import {server} from "../server.js"

const PORT = 8000;

server.listen(PORT, ()=>{           // tell Server which port to listen to, can also have a callback to add e.g. a ConLog
    console.log(`I'm listening on port ${PORT}`)
  }); 
```
-> run the program with "node ."
-> Reload server everytime something changes

* usually a lot of the node server-code is managed by frameworks like express.js
* library "supertest" requests an imported serverobject 

continuation of https://github.com/mntzd/notebook/blob/main/backend/basics.md
