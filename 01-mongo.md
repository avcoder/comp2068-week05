[Slide - Express steps]()

# getmdl.io portfolio template
- split into partials
- change link from styles.css to /stylesheets/style.css
- move images 
- make images show by going to style.css and changing all references from images to /images
- feel free to change picture with my twitter pic
- change style.css from png to jpg
- add border-radius: 50%

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

[Slide - How does our node app know about our mongodb?]()

[Slide - Mongoose]()

[Slide - Purpose of Schema]()

[Slide - npm i mongoose]()

# Creating variables.env
- in root folder create `variables.env` file
- Add entry: `DATABASE=mongodb://<dbuser>:<dbpassword>@ds251240.mlab.com:51240/retro`
- in mlab.com, click Users tab and create a user and password
- in variables.env, replace dbuser and dbpassword with credentials

# In app.js

`npm i dotenv`

```js
// use mongoose to connect to mongodb
require('dotenv').config({ path: 'variables.env' });
const mongoose = require('mongoose');
mongoose.connect(process.env.DATABASE);
```

## Build a mongoose schema

1.  Create a models folder
1.  In it, create Game.js, create schema, and export it as a mongoose.model

  ```js
  /* Game.js */
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
1. Edit games.ejs to use games data
  ```html
  <% include partials/header.ejs %>
      <h1>
          <%= title %>
      </h1>

      <div class="mdl-grid portfolio-max-width">

          <% for (let i = 0; i < games.length; i++) { %>
              <div class="mdl-cell mdl-card mdl-shadow--4dp portfolio-card">
                  <div class="mdl-card__media">

                      <img class="article-image" src="<%= games[i].imageUrl %>" border="0" alt="Game cover image">

                  </div>
                  <div class="mdl-card__title">
                      <h2 class="mdl-card__title-text">
                          <%= games[i].name %>
                      </h2>
                  </div>
                  <div class="mdl-card__supporting-text">
                      <%= games[i].publisher %>
                  </div>
                  <div class="mdl-card__actions mdl-card--border">
                      <a class="mdl-button mdl-button--colored mdl-js-button mdl-js-ripple-effect mdl-button--accent" href='/playgame?game=<%= games[i].imageUrl.substring(games[i].imageUrl.lastIndexOf("/")+1) %>'>Play</a>
                  </div>
              </div>
              <% } %>
      </div>

      <% include partials/footer.ejs %>
  ```

# Take care of is_active
```html
<%= isActive === 'portfolio' ? 'is-active' : '' %>
```

# Put / in gamesController

# Create add form

# Create admin table
h1 { text-align: center}
table { margin: 0 auto;}
remove classes for games[i].title (make sure model has correct var names)

# Add form
