# Building RESTful APIs with Node.js and Express

## Ben Allan-Rahill

link to the course is [here](https://www.linkedin.com/learning/building-restful-apis-with-node-js-and-express)

### HTTP Requests:

1. GET
   1. For **retrieving** data
2. PUT
   1. for **updating** data
3. POST
   1. for adding **new** data
4. DELETE
   1. for **removing** data

### Backend folder structure example:

```
src/
    controllers/
    models/
    routes/

server.js
```

## Working with Mongoose

```bash
npm i -S mongoose
```

### Working with Schema

Schema defines the rules for the pieces of data

do this in the model file

example schema:

```JavaScript
import mongoose from "mongoose";

const { Schema } = mongoose;

export const QuoteSchema = new Schema({
  who: {
    type: String,
    required: "Enter who said it",
  },
  what: {
    type: String,
    required: "Enter what was said",
  },
  created_date: {
    type: Date,
    default: Date.now,
  },
});
```

#### Controllers

example:

```javascript
import mongoose from "mongoose";
import { QuoteSchema } from "../models/Model";

// constructor
const Quote = mongoose.model("Quote", QuoteSchema, "quotes");

export const addNewQuote = (req, res) => {
  let newQuote = new Quote(req.body);

  newQuote.save((err, quote) => {
    if (err) {
      res.send(err);
    }
    res.json(quote);
  });
};
```
