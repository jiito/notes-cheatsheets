# Notes for MERN Web Development

## Author: Benjamin Allan-Rahill

## 3 Nodes

- Web server
  - for server rendering and specifying routes
- React components (front-end and back-end)
- API server

### Update NPM

```bash
sudo npm install -g npm
```

## Project Dependencies

1. First step: create package.json file

   1. This can be done using `npm init`

      1. Keep default of add answers to prompts

         e.g.

         ```bash
         package name: (quote-book)
         version: (1.0.0)
         description: This is a simple web app to keep track of quotes
         entry point: (index.js)
         test command:
         git repository: (https://github.com/benjamin-allanrahill/quote-book.git)
         keywords:
         author: Benjamin Allan-Rahill
         license: (ISC)
         About to write to /Users/ballanrahill/Desktop/projects/quote-book/package.json:

         {
         "name": "quote-book",
         "version": "1.0.0",
         "description": "This is a simple web app to keep track of quotes ",
         "main": "index.js",
         "scripts": {
             "test": "echo \"Error: no test specified\" && exit 1"
         },
         "repository": {
             "type": "git",
             "url": "git+https://github.com/benjamin-allanrahill/quote-book.git"
         },
         "author": "Benjamin Allan-Rahill",
         "license": "ISC",
         "bugs": {
             "url": "https://github.com/benjamin-allanrahill/quote-book/issues"
         },
         "homepage": "https://github.com/benjamin-allanrahill/quote-book#readme"
         }
         ```


            Is this OK? (yes) yes
            ```
       1. going to have "main" and "dev" dependencies

### Main dependencies

These dependencies will be used in production

- Express.js
- MongoDB
- React
- React-DOM
- prop-types
- EJS

### Dev dependencies

these can be installed using

```bash
npm i -D pkg-name
```

- Webpack
- Webpack-cli
- json-loader (actaully deprecated in new )
- Babel
  - Babel-loader
  - @babel/node
  - @babel/core
  - @babel/preset-env
  - @babel/preset-react
  - @babel/plugin-proposal-class-properties
- Nodemon
- ESLint
  - eslint
  - babel-eslint
  - eslint-plugin-react
  - eslint-config-airbnb
  - eslint-plugin-import
- Prettier
  - eslint-config-prettier
  - eslint-plugin-prettier

## Project Structure

Directories

- src
  - where modular code goes
- public
  - static pages
    - HTML
    - CSS
    - JS
- api
  - backend server

## NPM Scripts

found in package.json

good example from [here](https://www.linkedin.com/learning/learning-full-stack-javascript-development-mongodb-node-and-react/project-structure-and-configurations?u=2213609)

```json
"scripts": {
"start": "nodemon --exec babel-node server.js --ignore public/",
"dev": "webpack -wd"
}
```

## Webpack

Webpack is a bundler for the modular code

Webpack uses **Babel** as a loader to translate the code from modern syntax

### Webpack Configuration

example found [here](https://www.linkedin.com/learning/learning-full-stack-javascript-development-mongodb-node-and-react/project-structure-and-configurations?u=2213609) on LinkedIn Learning

```js
const path = require("path");

module.exports = {
  entry: "/src/index.js",
  output: {
    path: path.resolve("public"),
    filename: "bundle.js",
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
        },
      },
    ],
  },
};
```

### Babel configuration

example found [here](https://www.linkedin.com/learning/learning-full-stack-javascript-development-mongodb-node-and-react/project-structure-and-configurations?u=2213609) on LinkedIn Learning

```js
module.exports = {
  presets: ["@babel/react", "@babel/env"],
  plugins: ["@babel/plugin-proposal-class-properties"],
};
```

### ESLint configuration (with Prettier)

example found [here](https://www.linkedin.com/learning/learning-full-stack-javascript-development-mongodb-node-and-react/project-structure-and-configurations?u=2213609) on LinkedIn Learning

can use

```bash
npx eslint --init
```

use these files to configure the formatters

**.eslintrc**

```json
{
  "parser": "babel-eslint",
  "env": {
    "browser": true,
    "es6": true,
    "node": true,
    "jest": true
  },
  "extends": [
    "airbnb-base",
    "prettier",
    "eslint:recommended",
    "plugin:react/recommended"
  ],
  "parserOptions": {
    "ecmaVersion": 2020,
    "ecmaFeatures": {
      "jsx": true
    },
    "sourceType": "module",
    "codeFrame": false,
    "allowImportExportEverywhere": false
  },
  "plugins": ["react", "prettier", "import"],
  "rules": {
    "react/prop-types": ["warn"],
    "spaced-comment": ["error", "always", { "exceptions": ["-", "+"] }]
  }
}
```

link to configuring ESLint https://www.linkedin.com/learning/node-js-testing-and-code-quality/configuring-eslint?pathUrn=urn%3Ali%3AlyndaLearningPath%3A5b32b6d5498e4ef39c04c55c&u=2213609

**.prettierrc**

```json
{
  "trailingComma": "all",
  "printWidth": 100,
  "singleQuote": true,
  "semi": true,
  "tabWidth": 2
}
```

**Make sure to change the options in VSCode**

- Format on save
- default formatter

## Using Sass

1. Put styles in source directory (./sass)
2. npm i -S node-sass-middleware
3. Import and use in server.js

```javascript
server.use(
  sassMiddleware({
    src: path.join(__dirname, "sass"),
    dest: path.join(__dirname, "public"),
  })
);
```

## Reading from the state

link to [video](https://www.linkedin.com/learning/learning-full-stack-javascript-development-mongodb-node-and-react/reading-from-the-state?u=2213609)

- need to place objects on state
- proper place to do any modification is in componentDidMount

# Axios (getting data from the API)

[github repo](https://github.com/axios/axios)

```bash
npm i -S axios
```

## Server rendering initial data

video link [here](https://www.linkedin.com/learning/learning-full-stack-javascript-development-mongodb-node-and-react/server-rendering-with-reactdomserver?u=2213609)

1. Have a serverRender.js that helps get and render the data
2. Make sure the components allow for initial data

## Steps to follow

1. Configure development environment
2. Build the server
3. Build the API endpoints

## Adding Users

Following this example here https://blog.bitsrc.io/build-a-login-auth-app-with-mern-stack-part-1-c405048e3669

### Setting up that backend

#### Packages

- [`bcryptjs`](https://www.npmjs.com/package/bcryptjs): used to hash passwords before we store them in our database
- [`body-parser`](https://www.npmjs.com/package/body-parser): used to parse incoming request bodies in a middleware
- [`concurrently`](https://www.npmjs.com/package/concurrently): allows us to run our backend and frontend concurrently and on different ports
- [`jsonwebtoken`](https://www.npmjs.com/package/jsonwebtoken): used for authorization
- [`passport`](https://www.npmjs.com/package/passport): used to authenticate requests, which it does through an extensible set of plugins known as strategies
- [`passport-jwt`](https://www.npmjs.com/package/passport-jwt): passport strategy for authenticating with a JSON Web Token (JWT); lets you authenticate endpoints using a JWT
- [`validator`](https://www.npmjs.com/package/validator): used to validate inputs (e.g. check for valid email format, confirming passwords match)

#### Create the User Schema

**ex:**

```javascript
const mongoose = require("mongoose");
const Schema = mongoose.Schema;
// Create Schema
const UserSchema = new Schema({
  name: {
    type: String,
    required: true,
  },
  email: {
    type: String,
    required: true,
  },
  password: {
    type: String,
    required: true,
  },
  date: {
    type: Date,
    default: Date.now,
  },
});
module.exports = User = mongoose.model("users", UserSchema);
```

#### Set up form validation

an example for registering users:

```javascript
const Validator = require("validator");
const isEmpty = require("is-empty");
module.exports = function validateRegisterInput(data) {
  let errors = {};
  // Convert empty fields to an empty string so we can use validator functions
  data.name = !isEmpty(data.name) ? data.name : "";
  data.email = !isEmpty(data.email) ? data.email : "";
  data.password = !isEmpty(data.password) ? data.password : "";
  data.password2 = !isEmpty(data.password2) ? data.password2 : "";
  // Name checks
  if (Validator.isEmpty(data.name)) {
    errors.name = "Name field is required";
  }
  // Email checks
  if (Validator.isEmpty(data.email)) {
    errors.email = "Email field is required";
  } else if (!Validator.isEmail(data.email)) {
    errors.email = "Email is invalid";
  }
  // Password checks
  if (Validator.isEmpty(data.password)) {
    errors.password = "Password field is required";
  }
  if (Validator.isEmpty(data.password2)) {
    errors.password2 = "Confirm password field is required";
  }
  if (!Validator.isLength(data.password, { min: 6, max: 30 })) {
    errors.password = "Password must be at least 6 characters";
  }
  if (!Validator.equals(data.password, data.password2)) {
    errors.password2 = "Passwords must match";
  }
  return {
    errors,
    isValid: isEmpty(errors),
  };
};
```

#### Creating the Login endpoint

- Pull the errors and isValid variables from our validateLoginInput(req.body) function and check input validation
- If valid input, use MongoDB’s User.findOne() to see if the user exists
- If user exists, use bcryptjs to compare submitted password with hashed password in our database
- If passwords match, create our JWT Payload
- Sign our jwt, including our payload, keys.secretOrKey from keys.js, and setting a expiresIn time (in seconds)
- If successful, append the token to a Bearer string (remember in our passport.js file, we setopts.jwtFromRequest = ExtractJwt.fromAuthHeaderAsBearerToken();)

## Questions

- What is the difference between a router and the server?
