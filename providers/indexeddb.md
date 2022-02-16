---
description: That's right. JOSH... in your BROWSER! OMG!
---

# IndexedDB

IndexedDB is an API that's common to all browsers (except, as usual, Opera Mini because it supports nothing, and IE11 because it should die in a fire). With the IndexedDB provider, you can literally store data persistently in a browser - for your website built with React, Vue, jQuery... whatever it is, it can access the browser IndexedDB and you can use it with JOSH

{% hint style="info" %}
There are not provider options with the IndexedDB provider, but an empty option object must still be given.
{% endhint %}

### Using with Webpack

To use with Webpack, install with your project:

```
npm i @joshdb/indexeddb
** OR **
yarn add @joshdb/indexeddb
```

Then, in your code, use it as necessary:

```javascript
const Josh = require('@joshdb/core');
const JoshIndexedDB = require('@joshdb/indexeddb');

const db = new Josh({
  name: 'testing',
  provider: JoshIndexedDB,
  providerOptions: {},
});

db.defer.then(async () => {
  console.log(`Connected, there are ${await db.size} rows in the database.`);
});
```

### Using from a CDN (Directly in your website)

```markup
<script src="https://unpkg.com/@joshdb/core"></script>
<script src="https://unpkg.com/@joshdb/indexeddb@latest/dist/main.js"></script>
<script>
  const Josh = require('josh');
  const JoshIndexedDB = require('@joshdb/indexeddb');

  const db = new Josh({
    name: 'testing',
    provider: JoshIndexedDB,
    providerOptions: {},
  });

  db.defer.then(async () => {
    console.log(`Connected, there are ${await db.size} rows in the database.`);
  });
</script>
```

