Source for this page is [here](https://github.com/RealShadowNova/josh-examples/blob/master/typescript/quick-usage-example.md)

Josh is compatible with Typescript, we are constantly updating the types as soon as new features or modifications are added to assure you have no issues on your end.

## NOTICE!
Josh is still in Alpha. This example may not be up to date at all times.

### Importing a Josh and Initiating a Josh

```ts
// You can simply import Josh here.
// Josh is default exported no need to destructure.
import Josh from "josh";

// We use generic types to ensure the return type.
// This way we aren't using Typescript for nothing always using an 'any' type.

// You can set the generic to whatever you want stored.
// As an example we will store an array of strings.
const db = new Josh<string[]>({
  name: "example",
  provider: "@josh-providers/sqlite",
});

// Don't want a strong-typed Josh? You can!
// Simply don't use a generic type, the default generic is 'unknown'.
const db = new Josh({
  name: "example",
  provider: "@josh-providers/sqlite",
});

// Wait for the database to be ready.
(async () => {
  await db.defer;
  console.log(`Connected, there are ${await db.size} rows in the database.`);
})();
```

### Basic usage

```ts
// Josh methods are async, so make sure to always be in an asynchronous scope.
(async () => {
  // Setting data.

  // Supports simple strings
  await db.set("somestring", "This is a simple string value");

  // Supports arrays
  await db.set("anarray", [1, 2, 3, 4, 5]);

  // Supports arrays of objects
  await db.set("arrofobj", [
    { a: 1, b: 2 },
    { c: 3, d: 4 },
  ]);

  // Supports objects (obviously, the name is a dead giveaway!)
  await db.set("object", {
    id: 123345,
    name: "Josh Grow Ban",
    description: "Some dude",
  });

  // Supports setting object properties using paths
  await db.set("object.description", "A most awesome dude");

  // Supports setting things in arrays by index
  await db.set("anarray.0", "one"); // [ 'one', 2, 3, 4, 5 ]

  // Getting data.
  await db.get("somestring"); // "This is a simple string value"
  await db.get("anarray"); // [1, 2, 3, 4, 5]
  await db.get("anarray.0"); // 1
  await db.get("object.name"); // "Josh Grow Ban"

  // Deleting data.
  await db.delete(db.all); // CLEARS THE ENTIRE DATABASE
  await db.delete("string"); // deletes one key
  await db.delete("object.description"); // deletes one object property by path
  await db.delete("arrayofobj.1"); // deletes one array element by index
})();
```
