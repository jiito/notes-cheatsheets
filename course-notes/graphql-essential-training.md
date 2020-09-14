# GraphQL Essential Training

## Basic GraphQL Schema

Schema defines type

Resolver gets the data

example schema

```js
import { buildSchema } from "graphql";

const schema = buildSchema(`
    type Friend {
        id: ID
        firstName: String
        lastName: String
        gender: String
        emails: [Email]!
    }

    type Email {
        email: String
    }

    type Query {
        friend: Friend
    }
`);

export default schema;
```

resolver is just a function that returns the data
