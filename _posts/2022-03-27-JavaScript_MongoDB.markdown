---
layout: default
title: "JavaScript: MongoDB"
date: 2022-03-27 22:00:00
categories: JavaScript
---

### What is MongoDB?

- MongoDB is an open-source database program that organizes data by using documents.
  - Uses JSON-like documents with optional schemas.
  - Uses key-value pairing to associate data objects with properties.
- MongoDB Atlas is the global cloud database on AWS, Azure, and GCP
- MongoDB also has an ORM that is called Mongoose.

### NoSQL Databases (SQL VS NOSQL)

- SQL - Structured data schema(Strict) & data is set to several tables linked with a 'relationship'
- NoSQL - No Schema, No relationship, and Json-like data format

#### Commands

- Use {dbname} – Create db (if it doesn’t exist) & switch to specific db
  You won’t see your new database in the list of databases until data is added.

- Specify a collection name: data model, storing all documents related to that model within the same grouping.
  e.g. within recipe app (db), contacts (colllection), and data (documents)

- Insert
  db.inventory.insertOne
  db.inventory.insertMany

- Find
  find({key:”value”}) / findOne or findMany
  db.contacts.find({\_id: ObjectId("6241cb3b6d1c4b70d50a75b1")})
  db.contacts.find({name:"Jon"})

- Delete
  db.collection.deleteMany()
  db.collection.deleteOne()

- Update
  What is the use of set in MongoDB?
  In MongoDB, the $set operator is used to replace the value of a field to the specified value.

```javascript
Syntax: , { $set: { <field1>: <value1>, ... } }
db.contacts.update({name:"jon wexler"}, {$set:{email:”jonjwexler@gmail.com”}})
```

### Setting up Mongoose with your Node.js application

- select a db: use choose_db
- show all dbs: show dbs
- show collections in a db: use choose_db then show collections
- show all records in a db: use choose_db then db.users.find()
- delete a db: use choose_db then db.dropDatabase()
- to see which db is being used: db

#### Index.js (main.js)

```javascript
const express = require("express");
const mongoose = require("mongoose");
const app = express();
const port = 3000;

/**
 * Connect to our Mongo DB
 * We are returned a promise; then & catch
 * tells what to do when it succeeds .(then) and
 * what to do when it fails (.catch)
 */
mongoose
  .connect("mongodb://localhost:27017/usersDB2", {
    useNewUrlParser: true,
  })
  .then((data) => {
    console.log("Mongo DB connection success!");
  })
  .catch((err) => {
    console.log("Mongo DB connection failed: " + err.message);
  });

// Create a schema
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  fav_pizza: String,
  personalities: [String],
});

// Apply it to a model
const User = mongoose.model("User", userSchema);
// User has to be with capital first letter. mongo will make that small and pluralize
// the model name: "User" => "users"

// Creating

const pj = new User({
  name: "PJ",
  email: "BIGID@gmail.com",
  fav_pizza: "Pepperoni",
  personalities: ["Challenging","Kind"],
});

const hj = new User({
  name: "Hyukjoo Lee",
  email: "jaydon.lee@gmail.com",
  fav_pizza: "Pepperoni",
  personalities: ["Dedicated", "Detailed"],
});

const cr = new User({
  name: "Chaeryeong Kim",
  email: "k95c03r13@gmail.com",
  fav_pizza: "Hawaiian",
  personalities: ["Spontaneous", "Energetic"
});

User.insertMany([pj, hj, cr], function (err) {
  if (err) {
    console.log(err);
  } else {
    console.log("Successfully created db");
  }
});

// Create a simple path for the home page
// Will take the usual request, response,
// and next arguments needed for this sort of function

app.use("/", (req, res, next) => {
  res.json({
    confirmation: "success",
    data: "This is the mongo project!",
  });
});

app.listen(() => {
  console.log("app is listening " + port);
});

```

### Creating a schema

- As mentioned, MongoDB itself is a schema-less database. However, Mongoose enforces schemas on our behalf to help maintain data integrity.

ORM – Object Relational Mapping

#### Read.js

```javascript
const mongoose = require("mongoose");

//create and/or connect to a db
mongoose.connect("mongodb://localhost:27017/usersDB2", {
  useNewUrlParser: true,
});

// Create a schema
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  fav_pizza: String,
  personalities: [String],
});

// Apply it to a model
const User = mongoose.model("User", userSchema);
// User has to be with capital first letter. mongo will make that small and pluralize
// the model name: "User" => "users"

// Read All Data
User.find(function (err, users) {
  if (err) {
    console.log(err);
  } else {
    // console.log(users);
    // if we want to show only the names the following code does
    users.forEach(function (user) {
      console.log(user);
      // closing the connection: good practice
      mongoose.connection.close();
    });
  }
});
```

#### Update.js

```javascript
User.updateOne(
  { _id: "624210c0601f212f1c76367e" },
  { name: "CRK updated" },
  function (err) {
    if (err) {
      console.log(err);
    } else {
      console.log("marking");
    }
  }
);
```

#### Delete.js

```javascript
User.deleteOne({ _id: "624210c0601f212f1c76367e" }, function (err) {
  if (err) {
    console.log(err);
  } else {
    console.log("deleted");
  }
});
```
