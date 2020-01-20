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
```javascript
const fs = require("fs");

const files = fs.readdirSync("./"); // done synchronously 

// a-sync
fs.readdir("./", (err, files) => {
    if (err){
        throw err;
    }
    console.log("complete");

})
```

### Read files 

```javascript 
const fs = require("fs");

//synchron
const text = fs.readFileSync(PATH);
console.log(text);

fs.readFile(PATH, "UTF-8", (err, text) => {
    if (err) {
        throw err;
    }
    console.log(text)

});

// image read into a buffer  (do not supply encoding)
fs.readFile(IMAGE, (err, img) => {

});
```

### write and append files 

```javascript

const fs = require("fs");

const md = `
# this is a new file 

We can write test to a file with fs.writeFile

`;

fs.writeFile(PATH, md.trim(), err => {
    if (err) {
        throw err;
    }
    console.log("File saved.")
});

```

### Directory Creation

```javascript 
const fs = require("fs");

// check existence 
if (fs.existsSync(NAME)) {

} else {
    fs.mkdir(NAME, err => {
    if (err){
        throw err;
    }

    console.log("done")
});
};

```

### Append Files 

```javascript
const fs = require("fs");

fs.append(PATH, VAR);
```

### rename and remove files
```javascript 
const fs = require("fs");

fs.renameSync("NAME", "NEW NAME");

fs.rename("NAME", "NEW NAME", (err) => {

});

setTimeout(() => {
    fs.unlinkSync("NAME"); //delete
}, 4000); //4 seconds

```

### remove dir
```javascript

fs.readdirSync(PATH).forEach(fileName => {
    fs.unlinkSync(fileName);
})
fs.rmdir(NAME, (err) => {

});
```

## Files and Streams

### Readable File Streams

```javascript
const fs = require("fs");

const readStream = fs.createReadStream(PATH, ENCODING);