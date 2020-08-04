# Basic Usage

\[ TBD \] - Documentation isn't yet ready fully but here's a few examples: 

```javascript
const Josh = require("josh");

const db = new Josh({
  name: 'testing',
  provider: '@josh-providers/sqlite',
});

// defer resolves when the database link is established!
db.defer.then( () => {

  // 'count' gives you the size/count/number of rows.
  console.log(`Connected, there are ${await db.size} rows in the database.`);
  
  // SETTING DATA
  
  // Supports simple strings
  db.set("somestring", "This is a simple string value");
  
  // Supports arrays
  db.set("anarray", [ 1, 2, 3, 4, 5 ]);
  
  // Supports arrays of objects
  db.set("arrofobj", [ { a: 1, b: 2 }, { c: 3, d: 4 } ]);
  
  // Supports objects (obviously, the name is a dead giveaway!)
  db.set("object", { id: 123345, name: "Josh Grow Ban", description: "Some dude" });
  
  // Supports setting object properties using paths
  db.set("object.description", "A most awesome dude");
  
  // Supports setting things in arrays by index
  db.set("anarray.0", "one"); // [ 'one', 2, 3, 4, 5 ]
  
  // GETTING DATA
  db.get("somestring"); // the string above
  db.get("anarray"); // ditto on the array
  db.get("anarray.0"); // supports paths and indexes, returns 'one' in this case
  db.get("object.name"); // supports paths in objects of course.
  
  // DELETING
  db.delete(db.all); // CLEARS THE ENTIRE DATABASE
  db.delete("string"); // deletes one key
  db.delete("object.description"); // deletes one object property by path
  db.delete("arrayofobj.1"); // deletes one array element by index
});
```

