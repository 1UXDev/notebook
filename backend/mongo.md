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

# Documents in Mongo
* can only use 16mb files, larger files have to be split up


```jsx
// Two Components: Upload and Image-List
// Two States: Images and UploadingState

// Uploader passes the images via setImages
// 

// access files user uploaded through a 
event.target.files
// if there are files, get the first image
files && setImage(files[0])

// append in a different function to FormData Object
// Post the FormData Object with the appended image

//check if ok
// --> Success Message -> setUploadingState("Done") + clear function 
// --> setImages(images) -> Update component state with the retrieved images
```

**Naming Convention:**
Service: Object, Array, Functionality --> Handling Stuff

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



# Backend MongoDB Atlas

## Learning Objectives

- [ ] Knowing what MongoDB Atlas is
  - [ ] Creating an account for Mongodb Atlas
  - [ ] Creating a cluster and database
  - [ ] Setting up database user and security settings
  - [ ] Connecting with local app
- [ ] Setting up vercel with MongoDB Atlas

---

## MongoDB Atlas Introduction

For now, we have only worked with a local database hosted on our computer. However, when we host an application e.g. on Vercel, we cannot use our local database for such external projects.

In order to access our database, we need to make it accessible from the internet. This is why we depend on external providers to host our database. We will use MongoDB Atlas, a cloud provider for mongo databases.

---

## Setting up a MongoDB Atlas account and database

Follow this guide to set up your MongoDB Atlas account and your first database.

1. Go to [the MongoDB Atlas homepage](https://www.mongodb.com/atlas/database) and choose "Try Free" to start the process.
2. Create an account by providing your data or sign up using Google.
3. You might need to verify your MongoDB email adress.
4. You might be asked to tell MongoDB Atlas something about your future usecases:

<img src="assets/images/atlas_tell-us-something.png" alt="Tell us something about yourself and your project" width="300px">

5. To create a cluster, choose
   1. `M0 Free`,
   2. `aws`, and
   3. `Frankfurt` and click on "Create".

<img src="assets/images/atlas_create-cluster.png" alt="Create a cluster" width="300px">

6. In the left-hand navigation, choose `Security > Quickstart` to generate a first user.
   1. Choose a username and a password.
   2. 🚨 Make sure to write down your password!
   3. Click on "Create User".

<img src="assets/images/atlas_generate-admin.png" alt="Generate an admin user" width="300px">

7. Scroll down to choose where you would like to connect from:
   1. Choose "My Local Environment".
   2. Click "Add My Current IP Adress".

<img src="assets/images/atlas_local-env.png" alt="Choose connection from local environment" width="300px">

8. In the left-hand navigation, choose `Security > Network Acess`.

<img src="assets/images/atlas_network-access.png" alt="Network access overview at the beginning" width="300px">

10. In the IP Access List, behind your IP Adress, click on "Edit".
11. In the pop-up window, click "Allow Access from Anywhere".

<img src="assets/images/atlas_allow-access-from-anywhere.png" alt="Allow access from anywhere" width="300px">

12. Your Network Access tab should now look like this:

<img src="assets/images/atlas_access-from-anywhere-finished.png" alt="Finished state after allowing access from anywhere" width="300px">

13. In the left-hand navigation, choose `Deployment > Database` which brings to this view:

<img src="assets/images/atlas_deploy-database.png" alt="Deploying the database overview" width="300px">

14. On the right side of your cluster's name (here "Cluster0"), click the "Connect" button.
15. In the pop-up window, click "Connect your application":

<img src="assets/images/atlas_connect-to-cluster_choose-connection-method.png" alt="Choose connection method" width="300px">

16. Create a database user with a username and a password:

<img src="assets/images/atlas_connect-to-cluster_create-database-user.png" alt="Create database user" width="300px">

17. You should now see this screen:

<img src="assets/images/atlas_connect-to-cluster_finished-database-user.png" alt="Database user was generated" width="300px">

18. Click on "Choose a connection method". You will see a screen similar to the following:

<img src="assets/images/atlas_connect-to-cluster_connection-method-finished.png" alt="Connection to cluster finished" width="300px">

19. Copy the MongoDB URI (in this case, `mongodb+srv://paul:<password>@cluster0.mu12zrz.mongodb.net/?retryWrites=true&w=majority`). You will need it in your application.
20. Note the hint below: `Replace <password> with the password for the paul user.`
    1.  This is the user you have just created one step back (NOT the admin from the beginning).

## Connect your application with MongoDB Atlas

Creating a connection between your application and the cloud database in MongoDB Atlas is now very easy.

> 💡 We assume your app already has a local database connected.

1. In the root of your project, create a new file `.env`.
2. In the `.env` file, insert a variable called `MONGODB_URI` and declare it with the MongoDB Atlas URI you have created when setting up your connection above.
   1. The `.env` should look like this: `MONGODB_URI=mongodb+srv://paul:<password>@cluster0.mu12zrz.mongodb.net/?retryWrites=true&w=majority`.
   2. Replace the `<password>` part with the password for your database user (in this case, the user is called "paul").
   3. Note that you have to remove the brackets `<>` around the password as well.
3. Add `.env` to the `.gitignore` file if not already included. You can now delete your `.env.local` file.

4. Restart the development server and check your browser: you can now read, create, update and delete entries from your cloud database hosted by MongoDB Atlas! 🎉
5. You can check the collections and documents of your database via `Deployment > Database > Collections`:

<img src="assets/images/atlas_view-collections.png" alt="View collections in MongoDB Atlas" width="300px">

---

## Vercel and MongoDB Atlas (environment variables)

When deploying an application to Vercel, the app is not able to connect with your cloud database. This is because the authentication information (user and password) is stored in a `.env` file which is only available to your local development environment.

This is why we need to provide Vercel with the access details.

1. In the dashboard of your Vercel project, navigate to "Settings":

<img src="assets/images/vercel_project-navigation.png" alt="Vercel Dashboard Navigation" width="300px">

2. In the left-hand navigation, choose "Environment Variables".
   1. Add the key (`MONGODB_URI`) and the value (`mongodb+srv...`)
   2. Tick all environments (Production, Preview, and Development).
   3. Click "Save".

<img src="assets/images/vercel_setting-environment-variables.png" alt="Set the environment variables on Vercel project" width="300px">

3. At the bottom of this page, you should now see a new environment variable:

<img src="assets/images/vercel_environment-variables-finished.png" alt="Enviroment variable on Vercel successfully saved" width="300px">

4. Redelpoy your application:
   1. In the main navigation, choose "Deployments".
   2. Open the three dots next to your last deployment and choose "Redeploy".

<img src="assets/images/vercel_redeploy.png" alt="Redeploy project" width="300px">

5. If there's a popup, hit the "Redeploy" button again.

<img src="assets/images/vercel_redeploy-popup.png" alt="Redeploy project popup window" width="300px">

6. Congratulations, you are done! Open the Vercel URL of your project to see that your deployed application has now access to the cloud database.

> 📙 Read more about [how to set up environment variables in the Vercel docs](https://vercel.com/docs/concepts/projects/environment-variables).

## Resources

- [MongoDB Atlas Tutorial](https://www.mongodb.com/basics/mongodb-atlas-tutorial)
- [Environment Variables (Vercel Docs)](https://vercel.com/docs/concepts/projects/environment-variables)



