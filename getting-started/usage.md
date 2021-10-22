# Basic Usage

\[ TBD ] - Documentation isn't yet ready fully but here's a few examples:&#x20;

```javascript
const Josh = require("@joshdb/core");
const provider = require('@joshdb/sqlite');

const db = new Josh({
  name: 'testing',
  provider,
});

// this is an "IIFE", immediately invoked function expression.
(async () => {
  // 'count' gives you the size/count/number of rows.
  console.log(`Connected, there are ${await db.size} rows in the database.`);
  
  // SETTING DATA
  
  // Supports simple strings
  await db.set("somestring", "This is a simple string value");
  
  // Supports arrays
  await db.set("anarray", [ 1, 2, 3, 4, 5 ]);
  
  // Supports arrays of objects
  await db.set("arrofobj", [ { a: 1, b: 2 }, { c: 3, d: 4 } ]);
  
  // Supports objects (obviously, the name is a dead giveaway!)
  await db.set("object", { id: 123345, name: "Josh Grow Ban", description: "Some dude" });
  
  // Supports setting object properties using paths
  await db.set("object.description", "A most awesome dude");
  
  // Supports setting things in arrays by index
  await db.set("anarray.0", "one"); // [ 'one', 2, 3, 4, 5 ]
  
  // GETTING DATA
  await db.get("somestring"); // the string above
  await db.get("anarray"); // ditto on the array
  await db.get("anarray.0"); // supports paths and indexes, returns 'one' in this case
  await db.get("object.name"); // supports paths in objects of course.
  
  // DELETING
  await db.delete(db.all); // CLEARS THE ENTIRE DATABASE
  await db.delete("string"); // deletes one key
  await db.delete("object.description"); // deletes one object property by path
  await db.delete("arrayofobj.1"); // deletes one array element by index
})();
```
