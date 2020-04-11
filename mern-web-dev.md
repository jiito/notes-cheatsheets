# Notes for MERN Web Development 

## Author: Benjamin Allan-Rahill

## 3 Nodes 
* Web server 
* React components (front-end and back-end)
* API server 

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


            Is this OK? (yes) yes
            ```
       1. going to have "main" and "dev" dependencies 


### Main dependencies 
   * Express.js
   * 