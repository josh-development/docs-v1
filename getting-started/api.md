---
description: >-
  The full API documentation pulled directly from the source code via
  jsdocs-to-markdown.
---

# Josh API Documentation

## Josh

**Kind**: global class

* [Josh](api.md#Josh)
  * [new Josh\(\[options\]\)](api.md#new-josh-options)
  * [.keys](api.md#josh-keys-promise-less-than-array-string-greater-than) ⇒ `Promise.<Array.String>`
  * [.values](api.md#josh-values-promise-less-than-array-greater-than) ⇒ `Promise.<Array>`
  * [.size](api.md#josh-size-promise-less-than-number-greater-than) ⇒ `Promise.<number>`
  * [.get\(keyOrPath\)](api.md#josh-get-keyorpath-promise-less-than-greater-than) ⇒ `Promise.<*>`
  * [.getMany\(keysOrPaths\)](api.md#josh-getmany-keysorpaths-promise-less-than-array-less-than-array-greater-than-greater-than) ⇒ `Promise.<Array.<Array>>`
  * [.random\(count\)](api.md#josh-random-count-promise-less-than-array-less-than-array-greater-than-greater-than) ⇒ `Promise.<Array.<Array>>`
  * [.randomKey\(count\)](api.md#josh-randomkey-count-promise-less-than-array-less-than-string-greater-than-greater-than) ⇒ `Promise.<Array.<string>>`
  * [.has\(keyOrPath\)](api.md#josh-has-keyorpath-promise-less-than-boolean-greater-than) ⇒ `Promise.<boolean>`
  * [.set\(keyOrPath, value\)](api.md#josh-set-keyorpath-value-promise-less-than-josh-greater-than) ⇒ \[`Promise.<Josh>`\]
  * [.setMany\(data, overwrite\)](api.md#josh-setmany-data-overwrite-promise-less-than-josh-greater-than) ⇒ \[`Promise.<Josh>`\]
  * [.update\(keyOrPath, input\)](api.md#josh-update-keyorpath-input-promise-less-than-object-greater-than) ⇒ `Promise.<Object>`
  * [.ensure\(keyOrPath, defaultValue\)](api.md#josh-ensure-keyorpath-defaultvalue-promise-less-than-greater-than) ⇒ `Promise.<*>`
  * [.delete\(keyOrPath\)](api.md#josh-delete-keyorpath-promise-less-than-josh-greater-than) ⇒ \[`Promise.<Josh>`\]
  * [.push\(keyOrPath, value, allowDupes\)](api.md#josh-push-keyorpath-value-allowdupes-promise-less-than-josh-greater-than) ⇒ \[`Promise.<Josh>`\]
  * [.remove\(keyOrPath, value\)](api.md#josh-remove-keyorpath-value-promise-less-than-josh-greater-than) ⇒ \[`Promise.<Josh>`\]
  * [.inc\(keyOrPath\)](api.md#josh-inc-keyorpath-promise-less-than-josh-greater-than) ⇒ \[`Promise.<Josh>`\]
  * [.dec\(keyOrPath\)](api.md#josh-dec-keyorpath-promise-less-than-josh-greater-than) ⇒ \[`Promise.<Josh>`\]
  * [.find\(valueOrFn, path\)](api.md#josh-find-valueorfn-path-promise-less-than-array-greater-than) ⇒ `Promise.<Array>`
  * [.filter\(valueOrFn, path\)](api.md#josh-filter-valueorfn-path-promise-less-than-array-greater-than) ⇒ `Promise.<Array>`
  * [.autoId\(\)](api.md#josh-autoid-promise-less-than-string-greater-than) ⇒ `Promise.<string>`
  * [.import\(data, overwrite, clear\)](api.md#josh-import-data-overwrite-clear-promise-less-than-josh-greater-than) ⇒ \[`Promise.<Josh>`\]

### new Josh\(\[options\]\)

Initializes a new Josh, with options.

| Param | Type | Description |
| :--- | :--- | :--- |
| \[options\] | `Object` | Additional options an configurations. |
| \[options.name\] | `string` | Required. The name of the table in which to save the data. |
| \[options.provider\] | `string` | Required. A string with the name of the provider to use. Should not be already required, as Josh takes care of doing that for you. _Must_ be a valid provider that complies with the Provider API. The provider needs to be installed separately with yarn or npm. See [https://josh.evie.dev/providers](https://josh.evie.dev/providers) for details. |
| \[options.ensureProps\] | `boolean` | defaults to `true`. If enabled and an inserted value is an object, using ensure\(\) will also ensure that every property present in the default object will be added to the value, if it's absent. |
| \[options.autoEnsure\] | `*` | default is disabled. When provided a value, essentially runs ensure\(key, autoEnsure\) automatically so you don't have to. This is especially useful on get\(\), but will also apply on set\(\), and any array and object methods that interact with the database. |
| \[options.serializer\] | `function` | Optional. If a function is provided, it will execute on the data when it is written to the database. This is generally used to convert the value into a format that can be saved in the database, such as converting a complete class instance to just its ID. This function may return the value to be saved, or a promise that resolves to that value \(in other words, can be an async function\). |
| \[options.deserializer\] | `function` | Optional. If a function is provided, it will execute on the data when it is read from the database. This is generally used to convert the value from a stored ID into a more complex object. This function may return a value, or a promise that resolves to that value \(in other words, can be an async function\). |

**Example**

```javascript
const Josh = require("josh");
const provider = require("@josh-providers/sqlite");

// sqlite-based database, with default options
const sqliteDB = new Josh({
  name: 'mydatabase',
  provider,
});
```

### josh.keys ⇒ `Promise.<Array.String>`

Get all the keys in the database.

**Kind**: instance property of [`Josh`](api.md#josh)  
**Returns**: `Promise.<Array.String>` - An array of all the keys as string values.  


### josh.values ⇒ `Promise.<Array>`

Get all the values in the database.

**Kind**: instance property of [`Josh`](api.md#josh)  
**Returns**: `Promise.<Array>` - An array of all the values stored in the database.  


### josh.size ⇒ `Promise.<number>`

Get the amount of rows inside the database.

**Kind**: instance property of [`Josh`](api.md#josh)  
**Returns**: `Promise.<number>` - An integer equal to the amount of stored key/value pairs.  


### josh.get\(keyOrPath\) ⇒ `Promise.<*>`

Retrieves \(fetches\) a value from the database. If a simple key is provided, returns the value. If a path is provided, will only return the value at that path, if it exists.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: `Promise.<*>` - Returns the value for the key or the value found at the specified path.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrPath | `string` | Either a key, or full path, of the value you want to get. For more information on how path works, see [https://josh.evie.dev/path](https://josh.evie.dev/path) |

### josh.getMany\(keysOrPaths\) ⇒ `Promise.<Array.<Array>>`

Retrieve many values from the database. If you provide `josh.all` as a value \(josh being your variable for the database\), the entire data set is returned.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: `Promise.<Array.<Array>>` - An array of key/value pairs each in their own arrays. Each array element is comprised of the key and value: \[\['a', 1\], \['b', 2\], \['c', 3\]\] If paths are provided, the "key" is the full path.

| Param | Type | Description |
| :--- | :--- | :--- |
| keysOrPaths | `Array.<string>` \| `symbol` | An array of keys or paths to return, or `db.all` to retrieve them all. |

### josh.random\(count\) ⇒ `Promise.<Array.<Array>>`

Returns one or more random values from the database.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: `Promise.<Array.<Array>>` - An array of key/value pairs each in their own array. The array of values should never contain duplicates. If the requested count is higher than the number of rows in the database, only the available number of rows will be returned, in randomized order. Each array element is comprised of the key and value: \[\['a', 1\], \['b', 2\], \['c', 3\]\]

| Param | Type | Description |
| :--- | :--- | :--- |
| count | `number` | Defaults to 1. The number of random key/value pairs to get. |

### josh.randomKey\(count\) ⇒ `Promise.<Array.<string>>`

Returns one or more random keys from the database.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: `Promise.<Array.<string>>` - An array of string keys in a randomized order. The array of keys should never contain duplicates. If the requested count is higher than the number of rows in the database, only the available number of rows will be returned.

| Param | Type | Description |
| :--- | :--- | :--- |
| count | `number` | Defaults to 1. The number of random key/value pairs to get. |

### josh.has\(keyOrPath\) ⇒ `Promise.<boolean>`

Verifies whether a key, or a specific property of an object, exists at all.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: `Promise.<boolean>` - Whether the key, or property specified in the path, exists.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrPath | `string` | Either a key, or full path, of the value you want to get. For more information on how path works, see [https://josh.evie.dev/path](https://josh.evie.dev/path) |

### josh.set\(keyOrPath, value\) ⇒ [`Promise.<Josh>`](api.md#Josh)

Store a value in the database. If a simple key is provided, creates or overwrites the entire value with the new one provide. If a path is provided, and the stored value is an object, only the value at the path will be overwritten.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: [`Promise.<Josh>`](api.md#Josh) - This database wrapper, useful if you want to chain more instructions for Josh.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrPath | `string` | Either a key, or a full path, where you want to store the value. For more information on how path works, see [https://josh.evie.dev/path](https://josh.evie.dev/path) |
| value | `*` | The value to store for the key, or in the path, specified. All values MUST be "simple" javascript values: Numbers, Booleans, Strings, Arrays, Objects. If you want to store a "complex" thing such as an instance of a class, please use a Serializer to convert it to a storable value. |

### josh.setMany\(data, overwrite\) ⇒ [`Promise.<Josh>`](api.md#Josh)

Store many values at once in the database. DOES NOT SUPPORT PATHS. Or autoId.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: [`Promise.<Josh>`](api.md#Josh) - This database wrapper, useful if you want to chain more instructions for Josh.

| Param | Type | Description |
| :--- | :--- | :--- |
| data | `Array.<Array>` | The data to insert. Must be an array where each element is a \[key, value\] array. |
| overwrite | `boolean` | Whether to overwrite existing keys. Since this method does not support paths, existin data will be lost. |

**Example**

```javascript
josh.setMany([
  ["thinga", "majig"],
  ["foo", "bar"],
  ["isCool", true]
]);
```

### josh.update\(keyOrPath, input\) ⇒ `Promise.<Object>`

Update an object in the database with modified values. Similar to set\(\) except it does not overwrite the entire object. Instead, the data is _merged_ with the existing object. Object properties not included in your data are not touched.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: `Promise.<Object>` - The merged object that will be stored in the database.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrPath | `string` | Either a key, or full path, of the value you want to update. |
| input | `Object` \| `function` | Either the object, or a function. If a function is provided, it will receive the _current_ value as an argument. You are expected to return a modified object that will be stored in the database. |

**Example**

```javascript
josh.set('thing', {
  a: 1,
  b: 2,
  c: 3
});
josh.merge('thing', {
  a: 'one',
  d: 4
});
// value is now {a: 'one', b: 2, c: 3, d: 4}

josh.merge('thing', (previousValue) => {
  ...previousValue,
  b: 'two',
  e: 5,
});
// value is now {a: 'one', b: 'two', c: 3, d: 4, e: 5}
```

### josh.ensure\(keyOrPath, defaultValue\) ⇒ `Promise.<*>`

Returns the key's value, or the default given, ensuring that the data is there. This is a shortcut to "if josh doesn't have key, set it, then get it" which is a very common pattern.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: `Promise.<*>` - The value from the database for the key, or the default value provided for a new key.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrPath | `string` | Either a key, or full path, of the value you want to ensure. |
| defaultValue | `*` | Required. The value you want to save in the database and return as default. |

**Example**

```javascript
// Simply ensure the data exists (for using property methods):
josh.ensure("mykey", {some: "value", here: "as an example"});
josh.has("mykey"); // always returns true
josh.get("mykey", "here") // returns "as an example";

// Get the default value back in a variable:
const settings = mySettings.ensure("1234567890", defaultSettings);
console.log(settings) // josh's value for "1234567890" if it exists, otherwise the defaultSettings value.
```

### josh.delete\(keyOrPath\) ⇒ [`Promise.<Josh>`](api.md#Josh)

Remove a key/value pair, or the property and value at a specific path, or clear the database.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: [`Promise.<Josh>`](api.md#Josh) - This database wrapper, useful if you want to chain more instructions for Josh.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrPath | `string` \| `symbol` | Either a key, or full path, of the value you want to delete. If providing a path, only the value located at the path is deleted. Alternatively: josh.delete\(josh.all\) will clear the database of all data. |

### josh.push\(keyOrPath, value, allowDupes\) ⇒ [`Promise.<Josh>`](api.md#Josh)

Add a new value to an array.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: [`Promise.<Josh>`](api.md#Josh) - This database wrapper, useful if you want to chain more instructions for Josh.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| keyOrPath | `string` |  | Either a key, or full path, where the array where you want to add a value. |
| value | `*` |  | The value to add to the array. |
| allowDupes | `boolean` | `true` | Whether to allow duplicate values to be added. Note that if you're pushing objects or arrays, duplicates can occur no matter what, as detecting duplicate objects is CPU-intensive. |

### josh.remove\(keyOrPath, value\) ⇒ [`Promise.<Josh>`](api.md#Josh)

Remove a value from an array, by value \(simple values like strings and numbers\) or function \(complex values like arrays or objects\).

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: [`Promise.<Josh>`](api.md#Josh) - This database wrapper, useful if you want to chain more instructions for Josh.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrPath | `*` | Either a key, or full path, where the array where you want to remove from, is stored. |
| value | `*` \| `function` | Required. The value to remove from the array. OR a function to match a value stored in the array. If using a function, the function provides the value and must return a boolean that's true for the value you want to remove. |

**Example**

```javascript
// Assuming
josh.set('array', [1, 2, 3])
josh.set('objectarray', [{ a: 1, b: 2, c: 3 }, { d: 4, e: 5, f: 6 }])

josh.remove('array', 1); // value is now [2, 3]
josh.remove('objectarray', (value) => value.e === 5); // value is now [{ a: 1, b: 2, c: 3 }]
```

### josh.inc\(keyOrPath\) ⇒ [`Promise.<Josh>`](api.md#Josh)

Increments \(adds 1 to the number\) the stored value.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: [`Promise.<Josh>`](api.md#Josh) - This database wrapper, useful if you want to chain more instructions for Josh.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrPath | `*` | Either a key, or full path, to the value you want to increment. The value must be a number. |

### josh.dec\(keyOrPath\) ⇒ [`Promise.<Josh>`](api.md#Josh)

Decrements \(remove 1 from the number\) the stored value.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: [`Promise.<Josh>`](api.md#Josh) - This database wrapper, useful if you want to chain more instructions for Josh.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrPath | `*` | Either a key, or full path, to the value you want to decrement. The value must be a number. |

### josh.find\(valueOrFn, path\) ⇒ `Promise.<Array>`

Finds a value within the database, either through an exact value match, or a function. Useful for Objects and Array values, will not work on "simple" values like strings. Returns the first found match - if you need more than one result, use filter\(\) instead. Either a function OR a value **must** be provided.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: `Promise.<Array>` - Returns an array composed of the full value \(NOT the one at the path!\), and the key.

| Param | Type | Description |
| :--- | :--- | :--- |
| valueOrFn | `function` \| `string` | Mandatory. Either a function, or simple value. If using a function: it will run on either the stored value, OR the value at the path given if it's provided. - The function receives the value \(or value at the path\) as well the the key currently being checked. - The function must return a boolean or truthy/falsey value! Oh and the function can be async, too ;\) If using a value: - A path is mandatory when checking by value. - The value must be simple: string, boolean, integer. It cannot be an object or array. |
| path | `string` | Optional on functions, Mandatory on values. If provided, the function or value acts on what's at that path. |

**Example**

```javascript
// Assuming:
josh.set("john.shmidt", {
  fullName: "John Jacob Jingleheimer Schmidt",
  id: 12345,
  user: {
    username: "john.shmidt",
    firstName: "john",
    lastName: "shmidt",
    password: "somerandombcryptstringthingy",
    lastAccess: -22063545000,
    isActive: false,
    avatar: null,
  }
});

// Regular string find:
josh.find("john", "user.firstName")

// Simple function find:
josh.find(value => value.user.firstName === "john");

// Function find with a path:
josh.find(value => value === "john", "user.firstName");

// The return of all the above if the same:
["john.shmidt", {
  fullName: "John Jacob Jingleheimer Schmidt",
  id: 12345,
  user: {
    username: "john.shmidt",
    firstName: "john",
    lastName: "shmidt",
    password: "somerandombcryptstringthingy",
    lastAccess: -22063545000,
    isActive: false,
    avatar: null,
  }
}]
```

### josh.filter\(valueOrFn, path\) ⇒ `Promise.<Array>`

Filters for values within the database, either through an exact value match, or a function. Useful for Objects and Array values, will not work on "simple" values like strings. Returns all matches found - if you need a single value, use find\(\) instead. Either a function OR a value **must** be provided.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: `Promise.<Array>` - Returns an array composed of the full value \(NOT the one at the path!\), and the key.

| Param | Type | Description |
| :--- | :--- | :--- |
| valueOrFn | `function` \| `string` | Mandatory. Either a function, or simple value. If using a function: it will run on either the stored value, OR the value at the path given if it's provided. - The function receives the value \(or value at the path\) as well the the key currently being checked. - The function must return a boolean or truthy/falsey value! Oh and the function can be async, too ;\) If using a value: - A path is mandatory when checking by value. - The value must be simple: string, boolean, integer. It cannot be an object or array. |
| path | `string` | Optional on functions, Mandatory on values. If provided, the function or value acts on what's at that path. |

### josh.autoId\(\) ⇒ `Promise.<string>`

Get an automatic ID for insertion of a new record.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: `Promise.<string>` - A unique ID to insert data.  
**Example**

```javascript
const Josh = require("josh");
const provider = require("@josh-providers/sqlite");


const sqliteDB = new Josh({
  name: 'mydatabase',
  provider,
});
(async() => {
  const newId = await sqliteDB.autoId();
  console.log("Inserting new row with ID: ", newID);
  sqliteDB.set(newId, "This is a new test value");
})();
```

### josh.import\(data, overwrite, clear\) ⇒ [`Promise.<Josh>`](api.md#Josh)

Import an existing json export from josh or enmap. This data must have been exported from josh or enmap, and must be from a version that's equivalent or lower than where you're importing it.

**Kind**: instance method of [`Josh`](api.md#josh)  
**Returns**: [`Promise.<Josh>`](api.md#Josh) - This database wrapper, useful if you want to chain more instructions for Josh.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| data | `string` |  | The data to import to Josh. Must contain all the required fields provided by export\(\) |
| overwrite | `boolean` | `true` | Defaults to `true`. Whether to overwrite existing key/value data with incoming imported data |
| clear | `boolean` | `false` | Defaults to `false`. Whether to clear the enmap of all data before importing \(**WARNING**: Any exiting data will be lost! This cannot be undone.\) |

