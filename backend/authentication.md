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
