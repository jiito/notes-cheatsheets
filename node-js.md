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

### Write a file
```javascript
const
