---
description: >-
  A provider that Josh can use to communicate with a Mongo database using the
  mongodb module.
---

# MongoDB

### Installation

In your project folder, you should be able to just install using this command:

```text
npm i @joshdb/core @joshdb/mongo
** OR **
yarn add @joshdb/core @joshdb/mongo
```

### Usage

Using the mongo provider goes as such:

```javascript
const Josh = require("@joshdb/core");
const provider = require("@joshdb/mongo");

const myDb = new Josh({
  name: 'test',
  provider,
  providerOptions: {
    url: 'mongodb://localhost'
  }
});

db.defer.then( () => {
  console.log(`Connected, there are ${db.count} rows in the database.`);
});
```

### Provider Options

\[tbd\]

