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






