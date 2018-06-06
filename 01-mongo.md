[Slide - Why the Cloud]()

# Benefits of Cloud Hosting

- Faster performance
- Greater Scalability
- Economics - pay per use

## How is cloud hosting different from a traditional hosting platform like Dreamhost?

- For normal hosting companies, you'd pick a plan, (20$ per month) depending on storage, memory, bandwidth, servers
  [Slide - Olympics]()
- But if you go over that storage, it's like your cellphone, you pay for overage charges which are expensive
- And even if you reach a certain bandwith -> you don't get more bandwidth, so your site slows down

[Slide - demand spikes]()

- The problem is We get demand spikes. A lot of users at a certain time of year, we basically have to rent enough equipment so that we can always meet that maximum, which means we pay for that every month => $expensive, when most of the time we don't need that many resources
- Cloud hosting was designed to resolve these problems
- When spike occurs, another server(S) is spun up automatically to meet demand. Then vice versa
- So we don't pay a fixed cost any more, depends only on usage

## Cloud Service Companies

[Slide - Cloud companies]()

- There aren't that many cloud hosting companies because it's very expensive to expand to datacenters worldwide in order to meet spikes
- Amazon (AWS), Microsoft (Azure), Google Cloud, Heroku (5 free apps)
- https://medium.com/@GoRadialspark/heroku-alternatives-aws-azure-and-google-cloud-platform-870ae316527e

[Slide - Origins of NoSQL]()

# 3 problems with Relational DBs

1.  Scalability Problem with Relational databases: constantly having capacity problems as they got more and more data
1.  Serialization/Deserialization/ORM: Translating data from database into objects that our application code can use
1.  Flexibility: The relational model is inflexible especially when adding a new field or data rules change

[Slide - noSQL Solution]()

## NoSQL Alternative

- Vocabulary change: Relational databases store data in tables, whereas on noSQL databases like MongoDB, it stores data in collections.
- Vocabulary change: The noSQL equivalent of a relational database record is called a "document"
- In a collection, not every document has to look the same. Unlike traditional db where all records have to follow same structure

[Slide - Sample MongoDB Document]()

- Here is a restaurant object where all the data is stored as key/value pairs => JSON !
- Notice there is a unique identifier column that mongoDB automatically creates and populates called `_id`
- it gives it a data type of ObjectId and gives it a generated unique identifier, so we never have to setup any kind of unique keyfield since MongoDB will do this automatically
- Created in 2007 from the word "humongous", it's still the world's most popular noSQL db

[Slide - Schema-less]()

1.  Schema-less: Collections do not need to be defined before they can be used, 2 documents in the same collection can have a different number of fields, A collection can be automatically created when the first document is inserted into it
1.  Each document, can have a different format that evolves over time without requiring to modify document structure first
1.  Results in high performance and scalability

[Slide - master-child]()

1.  Data relations such as master-child data can now be nested, eliminating need for table relationships, foreign keys and joins
1.  Suited to cloud hosting solutions which can automatically scale on demand

# MongoDB

[Slide - Sample MongoDB Document]()

- To make it faster, instead of storing in plain text format, MongoDB will store it in Binary, in a format called BSON (Binary JSON)
- Here we have 2 grades nested in the master. Compare that to relational db.
- To query, no joins needed => fast
- Tradeoff, if there are more complex, nested relationships, that becomes hard to manage. So typically don't want to do this if there are lots of tables and relationships


## How do I get MongoDB?

- Download and install from https://www.mongodb.com/download-center#community
- Run in the cloud for free at https://www.mlab.com
- Enable as an Azure add-on

## Configuring mongoDB locally

- MongoDB is self contained and doesn't have any depedencies
- can copy all files from `c:\program files\mongodb\server\3.6\bin` to `c:\users\username\node\mongodb`
- it requires a `data` directory to store all data. The default is `c:\users\username\node\data\db`

# Create database and insert records

- Use mlab
- Create new > Plan-Type: Sandbox > Continue
- Name your db
- Add Collection > Name your collection

# How does our node app know about our mongodb?

# Introducing Mongoose

- Mongoose is an object-document mapper (ODM) that allows a node application to interface with a MongoDB database
- Mongoose is the node equivalent of Entity Framework (ORM) when connecting .NET and SQL SVR
- The way Node talks to MongoDB is via Mongoose which we'll install via npm

"Mongoose provides a straight-forward, schema-based solution to model your application data. It includes built-in type casting, validation, query building, business logic hooks and more, out of the box"

## Purpose of Mongoose Schema/Model

- To map a specific collection in a MongoDB for a Node application
- To set out validation rules for a MongoDB collection
- To allow a model class to use the built-in mongoose CRUD methods
- we create the models ourselves; these schemas live in the web app, not the db

## Installing mongoose then require it

`npm i mongoose`
[npm.im/mongoose](https://www.npmjs.com/package/mongoose)

## In a node application, where do we need to add a reference to mongoose?

- In app.js
- In any models we create
- In any controllers we create

## In app.js

`npm i dotenv`

```js
// use mongoose to connect to mongodb
require('dotenv').config({ path: 'variables.env' });
const mongoose = require('mongoose');
mongoose.connect(process.env.DATABASE);
```

## Build a mongoose schema

1.  Create a models folder
1.  In it, create game.js, create schema, and export it as a mongoose.model

  ```js
  /* game.js */
  const mongoose = require('mongoose');

  // define a schema for the game model
  // this and all other models inherit from mongoose.Schema

  const gameSchema = new mongoose.Schema({
    name: {
      type: String,
      required: 'Doh! You forgot to put in the game title for the name',
    },
    publisher: {
      type: String,
      required: 'Please enter publisher',
    },
    imageUrl: {
      type: String,
      required: 'Please enter URL of game cover image',
    },
    year: {
      type: Number
    }
  });

  // make the class public
  module.exports = mongoose.model('Game', gameSchema);
  ```
  * required field can include a message to give to user if they forgot to enter data for that field

1. Create /controllers/games.js
