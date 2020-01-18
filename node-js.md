# Node.js Notes

## Node Modules
### Core Modules 

``` javascript
const path = require("path");

// more intense logging
const { log } = require("util"); //destructuring
log(path.basename(__filename));
log(" ^ The name of the current file");

// v8
const v8 = require("v8")
util.log(v8.getHeapStatistics());
```

### Collect information with readline

``` javascript

const readline = require("readLine");

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.question("How do you like node? ", answer => {
    console.log(`Your answer: ${answer}`)
});
```

### Export custom modules 

```javascript
// exports Ben
module.exports = "Ben"

// eg 
let count = 0;

const inc = () => ++count;
const dec = () => --count;

const getCount = () => count;

module.exports = {
    inc,
    dec,
    getCount
};

// in another file 
const counter = require(PATH);

counter.inc();
console.log(counter.getCount());
```

### EventEmitter 

```javascript
const events = require("events");

const emitter = new events.EventEmitter();

emitter.on("customEvent", (message, user) => {
    console.log(`${user}: ${message}`)
});

emitter.emit("customEvent", "Hello World", "Computer");
emitter.emit("customEvent", "That's pretty cool huh?", "Ben");
```

## File System Basics 

### List directory files