## Building a Website with Node and Express 

### Anatomy of HTTP request 

"GET / --> give the index page of the webserver 

code 2xx --> everything is good 

POST --> send content with body of the request 

code 3xx -->redirection

code 4xx -->client error 

code 5xx --> server error 


### Creating a server with pure Node.js

```javascript
const http = require('http');
const url = require('url'); // help with parsing urls

function handler(req, res) {

    // with paths 
    const parsedUrl = url.parse(req.url, true);
    if (parsedUrl.pathname === '/'){
        res.writeHead(200, {'Content-type':'text/plain'}); // write http header
        res.write('Hello, I am a webserver!');
        return res.end();
    } else if (parsedUrl.pathname === '/hello') {
        const name = parsedUrl.query.name;
        if (!name) {
            res.writeHead(400, {'Content-type':'text/plain'});
            return res.end();
        }
        res.writeHead(200, {'Content-type':'text/plain'});
        res.write(`Hello ${name}`);
        return res.end();
    } else {
        res.writeHead(404, {'Content-type':'text/plain'})
        return res.end();
    }



}

const server = http.createServer(handler); //expects handler function (above)

server.listen(3000); //default port for node serv

```

### Creating a server with Express
```javascript

const express = require('express');

const app = express();

//middleware
app.use((req, res, next) => {
    res.setHeader('x-server-date', new Date());
});

//handlers 
app.get('/', (req, res, next) => {
    return res.send('Hello, I am a webserver');
});

app.get('/hello', (req, res, next) => {
    if (!req.query.name) {
        return res.status(400).end();
    }
    return res.send(`Hello ${req.query.name}`);
});

app.listen(3000);

