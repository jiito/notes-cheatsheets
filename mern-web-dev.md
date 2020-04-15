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

example request

## Steps to follow

1. Configure development environment
2. Build the server
3. Build the API endpoints

## Questions

- What is the difference between a router and the server?
