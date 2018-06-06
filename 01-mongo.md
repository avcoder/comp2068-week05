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

[Slide - noSQL Solution]()

[Slide - Sample MongoDB Document]()

[Slide - Schema-less]()

[Slide - master-child]()

[Slide - Sample MongoDB Document]()

[Slide - How do I get mongoDB]()

[Slide - mlab]()

[Slide - Retro games]()

[Slide - Add games]()

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
