# Parts Unlimited Backend

The Parts Unlimited backend is Node web app written with [Express](https://expressjs.com/)


## Prerequisites 
- You need to have [nodejs](https://nodejs.org/en/) version >= 15 installed. It is recommended to use [Node Version Manager](https://github.com/nvm-sh/nvm) if you need multiple nodejs versions installed locally.
- Use the NPM bundled with node to install [yarn](https://yarnpkg.com/getting-started)
- Install the application dependencies with `yarn install`

### Database

This application uses MongoDB. You can [install it directly](https://docs.mongodb.com/v5.0/installation/), or use [Docker](https://hub.docker.com/_/mongo). If you choose running via docker, spin up the instance using the `docker-compose.yml` file

```
docker-compose up -d
```

### Configuration

Create a `.env` file in this folder, with the following configuration -

```
MONGODB_URI=mongodb://localhost:27017/
```

Change the URI according to the way you run your local MongoDB instance. 

## Getting started

To start the app use: `yarn dev` from the backend directory.

Make sure your DB is up and running.

## Dependencies

- [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) - For generating JWTs used by authentication
- [mongoose](https://github.com/Automattic/mongoose) - For modeling and mapping MongoDB data to javascript
- [mongoose-unique-validator](https://github.com/blakehaswell/mongoose-unique-validator) - For handling unique validation errors in Mongoose. Mongoose only handles validation at the document level, so a unique index across a collection will throw an exception at the driver level. The `mongoose-unique-validator` plugin helps us by formatting the error like a normal mongoose `ValidationError`.
- [passport](https://github.com/jaredhanson/passport) - For handling user authentication
- [slug](https://github.com/dodo/node-slug) - For encoding titles into a URL-friendly format

## Application Structure

- `app.js` - The entry point to our application. This file defines our express server and connects it to MongoDB using mongoose. It also requires the routes and models we'll be using in the application.
- `config/` - This folder contains configuration for passport as well as a central location for configuration/environment variables.
- `routes/` - This folder contains the route definitions for our API.
- `models/` - This folder contains the schema definitions for our Mongoose models.

## Error Handling

In `routes/api/index.js`, we define a error-handling middleware for handling Mongoose's `ValidationError`. This middleware will respond with a 422 status code and format the response to have [error messages the clients can understand](https://github.com/gothinkster/realworld/blob/master/API.md#errors-and-status-codes)
