# 👶 Authentication Basics

### Authentication vs Authorization
Authorization: I allow the user to do something, like edit a button
Authentication: Making 

### hashing
creates a secure string e.g. for a password  != encryption
* cannot be decrypted to original input: even if an attacker has the hashed password from a DB, they cannot use it
* every entry is based on the entries before it
* has to be deterministic & fixed length

Sender hashes document > sends doc & HashString > Receiver hashes it again > if hashstrings are the same, the document was not altered

#### Salting || The problem with Lookup Tables
You can lookup hashes in a pre-hashed rainbow / lookup tables and might be able to match the hash-strings to get the original PW
-> **but not as easily if you salted your hashes**

```jsx
// hash.mjs       // has to be a module file
import bcyrpt from "bcrypt.js"

const pw="123456"
const salt = bcrypt.genSaltSync()       // random string that is prepended to the hash
const hash = bcrypt.hashSync(pw, salt)  // hashing is done with the Salt
console.log(hash)                       // returns a different hash everytime, since the Salt is always different 
// node hash.mjs
```

* The Salt could also be viewed by anyone, but the USP is, the hash is now pretty unique, so it will not turn up in RainbowTables
* PW in DB could look like this:  "S2acdsvfbgr23$NHD323?234dfNFN1Can§33nfmKJNKUOB" <br>
------------------------------| ---------- Salt ---------- | -- Salted & Hashed Password -- |

### encryption
#### Public Key Cryptography
* Key Pair of *private* and *public* key
* Public Key used to decrypt a message, that can only be decrypted with the receivers private Key
* If the Private Key becomes public, the whole communication is corrupted


## Szenario
1. User tries to log in with Mail & PW
2. For the Mail, the salted Hash is pulled from DB
3. Salt is stripped off to use it with the users typed PW
4. If the hash from the salted userInput is the same as in the DB --> Success


## Sign-Up process Example
**User:**
Post Request with Form Inputs in the Body
**Server:**
Check if its Post Request, Destructure email and password from Body
Create Salt in x Rounds
create hash
Create new user Doucment{email, password:hash)


<br>

------------------------

## Cookies
Client & Server communicate via httpRequest (http is stateless, there is no state between req-res-cycle)
-> But user being logged-in is a state
Server: is the request I'm getting from a user I already know?

### Server Sessions
?? A session exists between two states (req,res) ??
1. Server sets a Cookie, Response the Server sends contains the Cookie in the Header
2. Cookie is then placed in the users browser and sent with the Users future Requests
3. The Server checks whether the request and the sent cookie match up in the DB
4. Cookie can have an expiration date or can be deleted via Server-Response

### JWT - JSON webtoken
stateless form of authentication
* Information is sent back and forth in Webtoken, without storing anything in the DB

#### Set Cookie
Use Response Object, 
```jsx
res.setHeader("Set-Cookie", cookie.serialize("auth", user._id, {      // name of cookie, value
  httpOnly:true,                                                      // configure 
  secure: process.env.NODE_ENV !== "development"
  maxAge = 60*60*24*7 // when does it expire? -> means 1 week
  path"/"
}
res.status(200).json({})
```
-> reading cookies is very similar


### Middleware
??? something to do with the states inbetween request & response
--> Research 

<br>

---------------------

<br>

# 🚀 Authentication through Tools
IronSessions: Does the CookieSetting for you

## NextAuth.js
### Using oAuth
Another Application authorizes you

Pro: easy to use for users
Con: You do not have the e-Mail address of the user

```jsx
// in pages/api/auth/[...nextauth].js     // "..." gets all the auths
// npm install @next-auth/mongodb-adapter mongodb ...
import GitHubProvider from "next-auth/providers/github"
import clientPromise from "../../lib/dbconnect"

export const authOptions = {
  provider:[
    GithubProvider({
      clientId: process.env.GITHUB_ID,
      clientSecret: process.env.GITHUB_SECRET
    }),
  ],
  adapter: MongoDBAdapter(clientPromise),
}  

export default NextAuth(authOptions)
// adapters = for every storage you use, there is a different adapter (postgresql, mongo, ...)
```
-> Better Practice: ask user at least for username after oAuth

⚠️ The oAuth Provider wants to know when you are using their Service to Authenticate
1. Get "Client ID" and add to .env file -> GITHUB_ID
2. Get "Secret" (basically the password) -> 
3. Set Homepage URL
4. Authorization Callback URL "yourURL/api/auth"

```jsx
import {useSession, signIn, signOut} from "next-auth/react"

const {data:sessions} = useSession()     // get session
if(session){                            // do I have a logged in User?
  return(
    <h1>Hi {session.user.name}</h1>
    <button type="submit" onSubmit={signIn}>Sign In</button> // onSubmit calls the SignIn function from next-auth
   )
```


### Using EMail
Email-Provider sends "Magic Links"
-> could also be backup Auth-Method if users loses oAuth Account




