---
description: 'That''s right. You heard me. JSON Storage. Don''t try this at home, folks!'
---

# JSON

The fabled JSON storage is a strange beast - I myself have specifically told \*many\* people before that storing data in JSON files is _not_ an appropriate database. On the other hand, the reason I say this all the time is that people don't ever do it _correctly_. So... here's JSON storage done right, for your pleasure.

### Installation

To install the JSON provider, run the following:

```text
npm i @joshdb/json
** OR **
yarn add @joshdb/json
```

### Usage

Here's how you setup and use the JSON provider: 

```javascript
const Josh = require('@joshdb/core');
const JoshJSON = require('@joshdb/json');

const db = new Josh({
  name: 'testing',
  provider: JoshJSON,
  // See below for all provider options.
  providerOptions: {},
});

db.defer.then(async () => {
  console.log(`Connected, there are ${await db.size} rows in the database.`);
});
```

### Provider Options

\[TBD\]

