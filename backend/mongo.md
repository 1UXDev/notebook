# Mongo Basics

## Relational & Non-Relational DB's
**Relational DB's**
* stores data in tables
* normalization: we want to avoid duplicates in data
  * E.g. Multiple people work in same company, company address changes, all adresses in DB had to be changed :(
  * instead: Build another table with company adresses and build a relation between those tables
* Drawback: when you only need one attribute, e.g. HairColor for a few entries, you're adding the column for all entries

**Non relational DB's (NoSQL, Document Based, ...)
* Data is organized in documents (similar to json: bson)
* You can compute data on the fly (e.g. calculate age from birthday)

## Structure of Mongo
1. Database     (e.g. fish-shop)
2. 🛢 Collections  (e.g. products / users / ...)
3. 📁 Documents    (_id: ObjectId('12n345n4n5kb6543245jn6j4n3564k')
4. 📄 Fields       ( exist inside Documents)
```jsx
name: "Anemonefish"
description: "Nemo"
price: 65,
reviews: Array          // Array of reviews
    0: "2345678976543"    // String to review Document (a seperate collection)
    1: "2345678987653"    // Reviews could also be stored in an sql-like structure (writing the reviews directly in the Fields)
```
*entities* - Things that you want to store data of: e.g. users, tweets, images, ...

<br>

### How to structure?
Ask yourself:
do I only review the data? Do I update it? Do I need all the data everytime or only parts of it?

<br>

<br>

-----------------------

<br>


# Backend MongoDB

## Introduction: Databases

### What is a Database?

Let's recall what a server is:

- a program running 24/7 that is designed to **provide services to other computers or devices**,
- it can host a variety of services, such as a web server, an email server, a file server, or **a database server**,
- we have used Next.js API routes as a server to _serve_ data (from a `data.js` file in the same project).

Now consider what a database server is:

- it is a program that is specifically designed to **host and manage a database**,
- it manages the data stored in the database,
- it ensures that it is available to users and applications that need to access it.
- The data storage in a database is persistent.

### Relational vs. non-relational Databases

There are some [differences between relational and non-relational databases](https://www.mongodb.com/compare/relational-vs-non-relational-databases)
(aka SQL vs NoSQL):

**Relational**:

- data is stored in tables (like Excel, Numbers, Spreadsheets, …),
- the tables are connected to each other,
- constraint: we must decide for each column what we do if we don't have data for all entries in this column

**Non-relational**:

- data is stored in JSON-like structures,
- data is stored in key/value pairs,
- each data set in the database can have unique keys

> 💡 You can find an [in-depth explanation and comparison here](https://www.mongodb.com/compare/relational-vs-non-relational-databases).

---

## MongoDB

- As a non-relational database, MongoDB is less strict and easy to use.
- The name MongoDB comes from "hu_mongo_us" \_d_ata_b_ase.
- The name was chosen to reflect the scalability and flexibility of the database.

### MongoDB Terminology

**Database**:

- A MongoDB database is a collection of data that is organized and stored in a specific way, using the MongoDB database management system.
- A MongoDB database can have multiple sets of data called _collections_.

**Collection**:

- A collection is a grouping of MongoDB entries called _documents_.
- A collection is a equivalent of a table in a relational database system.
- A collection exists within a single database.

**Document**:

- A MongoDB document is a _JSON-like data structure that consists of key-value pairs_.
- Documents can have different _fields_.
- These key-value pairs are called _fields_.

**Field**:

- In MongoDB, a field is a _key-value_ pair that is stored in a _document_.
- The field key is a string that identifies the field, and the field value is the data stored in the field.

### MongoDB Queries

You can search your local MongoDB in MongoDB Compass. To do so, open the mongo shell at the bottom of the app.

Common commands:

- `dbs`: show all databases
- `db`: show name of current database
- `use jokes-database`: switch to the database called `jokes-database`

The following commands refer to a collection called `jokes`:
| | Query Methods (one) | Query Methods (many) |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| **C**reate | `db.jokes.insertOne({joke: "What's the action like at a circus? In-tents."})` | `db.jokes.insertMany([{…}, {…}])` |
| **R**ead | `db.jokes.findOne({_id: ObjectId("[paste_id_here]")})` | `db.jokes.find(…)` |
| **U**pdate | `db.jokes.updateOne({ _id: ObjectId("[paste_id_here]") }, { $set: { joke: "What's the action like at a circus? In-tents." } })` | `db.jokes.updateMany(…)` |
| **D**elete | `db.jokes.deleteOne({_id: ObjectId("[paste_id_here]")})` | `db.jokes.deleteMany(…)` |

> 📙 See the [MongoDB documentation](https://www.mongodb.com/docs/mongodb-shell/crud/) for details how to use the query methods.

---

## Database Design

General Guidance:

- Design your collections and documents around the data you need to store and the queries you need to perform.
- Use arrays to store lists of related data within a single document.
- Try to avoid deeply nested data structures. If your documents become too complex start to split the data into multiple collections and connect the data with references (see the example below).
- If you want to reference an object that is stored in a different collection, you can use foreign keys:
  - If you have a **users** collection and a **jokes** collection, you can use a foreign key in the **jokes** collection to store a reference to the user who created each joke.
  - This allows you to store information about the user who created each joke, without duplicating data in the jokes collection.

### Database Relationships

There are three different relationships between documents:

**One-To-One**

- A one-to-one relationship in MongoDB exists when one document in one collection is related to exactly one document in another collection.
- This can be implemented by storing a reference to the related document in any of the two collections. The direction does not matter in this case. One-to-one relationships only make sense in certain special cases. For simplicity sake, think about adding the fields of one collection into the other instead.

**One-To-Many**

- A one-to-many relationship in MongoDB exists when a document in one collection is related to multiple documents in another collection.
- This can be implemented by storing a reference to the "one" collection document in the connected "many" collection documents.

**Many-To-Many**

- A many-to-many relationship in MongoDB exists when multiple documents in one collection is related to multiple documents in another collection, and vice versa.
- This is usually achieved by creating an intermediary collection which documents have a reference to both connected collections (i.e. they are split into two one-to-many relationships).

> 📙 Read more about these [relationships in the MongoDB documentation](https://www.mongodb.com/docs/manual/tutorial/model-embedded-one-to-one-relationships-between-documents/).

### Example Visualization

The following three collections visualize the best practices and relationships mentioned above.

![Database Collections Example](assets/database_collections.png)

```json5
// Jokes collection:
{
  "_id": ObjectId("joke1ID"),
  "userId": ObjectId("user1ID"),
  "joke": "Why do programmers hate nature? It has too many bugs.",
}

// Users collection:
{
  "_id": ObjectId("user1ID"),
  "username": "jane.doe",
  "email": "jane.doe@example.com",
}

// Comments collection:
{
  "_id": ObjectId("comment1ID"),
  "jokeId": ObjectId("joke1ID"),
  "userId": ObjectId("user1ID"),
  "comment": "That's a good one!"
}
```

Notes:

- Each document in the collections has an `_id` field that is a unique identifier.
- Each joke document has a `joke` field that stores the text of the joke and a `userId` field that stores the ID of the user who created the joke. This establishes a **one-to-many** relationship between the joke and the user collection (one joke is owned by one user, but one user can own many jokes).

- Each user document has a `username` field that stores the user's username and an `email` field that stores the user's email address.

- Each comment document has a `jokeId` field that stores the ID of the joke that the comment is associated with, a `userId` field that stores the ID of the user who created the comment, and a `comment` field that stores the text of the comment.
- The `jokeId` field and `userId` field implement **one-to-many** relationships between the comments, jokes, and users collections, as a joke can have multiple comments and a user can create multiple comments, but each comment can only be associated with one joke and one user.

---

## Resources

- [Differences between relational and non-relational databases](https://www.mongodb.com/compare/relational-vs-non-relational-databases)
- [In-depth explanation and comparison relational/non-relational](https://www.mongodb.com/compare/relational-vs-non-relational-databases)
- [CRUD operations in MongoDB documentation](https://www.mongodb.com/docs/mongodb-shell/crud/)





