# Creating a Provider

So, you want to create your own provider? I'm too slow to make them, aren't I? Well, you're in luck, because I've made every attempt to document what's required for new providers to be built. Specifically, below is a list of methods that they need to support.

For examples of how these methods might work, please look at [existing providers](https://github.com/eslachance/josh-providers/) and their code. If you can make those methods more efficient or performant using core features of your database then by all means, feel free to do so! But, they must return the data in the format described in the code.

Note that the documentation below doesn't include example return values, but [the source code does](https://github.com/eslachance/josh-providers/docs/base\_provider.js).

## JoshProvider API

Every Josh Provider must contain a certain number of methods that will be called by the main Josh code.

If your provider does not support a method, it should be present and throw an error indicating this fact.

**Kind**: global class

* [JoshProvider](creating-a-provider.md#JoshProvider)
  * [new JoshProvider(\[options\])](creating-a-provider.md#new-joshprovider-options)
  * [.init(Josh)](creating-a-provider.md#joshprovider-init-josh-promise) ⇒ `Promise`
  * [.get(key, path)](creating-a-provider.md#joshprovider-get-key-path-promise-less-than-greater-than) ⇒ `Promise.<*>`
  * [.getAll()](creating-a-provider.md#joshprovider-getall-promise-less-than-object-less-than-greater-than-greater-than) ⇒ `Promise.<Object.<*>>`
  * [.getMany(keys)](creating-a-provider.md#joshprovider-getmany-keys-promise-less-than-object-less-than-greater-than-greater-than) ⇒ `Promise.<Object.<*>>`
  * [.random(count)](creating-a-provider.md#joshprovider-random-count-promise-less-than-object-less-than-greater-than-greater-than) ⇒ `Promise.<Object.<*>>`
  * [.randomKey(count)](creating-a-provider.md#joshprovider-randomkey-count-promise-less-than-array-less-than-string-greater-than-greater-than) ⇒ `Promise.<Array.<string>>`
  * [.has(key, path)](creating-a-provider.md#joshprovider-has-key-path-promise-less-than-boolean-greater-than) ⇒ `Promise.<boolean>`
  * [.keys()](creating-a-provider.md#joshprovider-keys-promise-less-than-array-less-than-string-greater-than-greater-than) ⇒ `Promise.<Array.<string>>`
  * [.values()](creating-a-provider.md#joshprovider-values-promise-less-than-array-less-than-greater-than-greater-than) ⇒ `Promise.<array.<*>>`
  * [.count()](creating-a-provider.md#joshprovider-count-promise-less-than-integer-greater-than) ⇒ `Promise.<integer>`
  * [.set(key, path, val)](creating-a-provider.md#joshprovider-set-key-path-val-promise-less-than-provider-greater-than) ⇒ `Promise.<Provider>`
  * [.setMany(data, overwrite)](creating-a-provider.md#joshprovider-setmany-data-overwrite-promise-less-than-provider-greater-than) ⇒ `Promise.<Provider>`
  * [.delete(key, path)](creating-a-provider.md#joshprovider-delete-key-path-promise-less-than-provider-greater-than) ⇒ `Promise.<Provider>`
  * [.clear()](creating-a-provider.md#joshprovider-clear-promise-less-than-provider-greater-than) ⇒ `Promise.<Provider>`
  * [.push(key, path, value, allowDupes)](creating-a-provider.md#joshprovider-push-key-path-value-allowdupes-promise-less-than-provider-greater-than) ⇒ `Promise.<Provider>`
  * [.remove(key, path, val)](creating-a-provider.md#joshprovider-remove-key-path-val-promise-less-than-provider-greater-than) ⇒ `Promise.<Provider>`
  * [.inc(key, path)](creating-a-provider.md#joshprovider-inc-key-path-promise-less-than-provider-greater-than) ⇒ `Promise.<Provider>`
  * [.dec(key, path)](creating-a-provider.md#joshprovider-dec-key-path-promise-less-than-provider-greater-than) ⇒ `Promise.<Provider>`
  * [.math(key, path, operation, operand)](creating-a-provider.md#joshprovider-math-key-path-operation-operand-promise-less-than-provider-greater-than) ⇒ `Promise.<Provider>`
  * [.findByFunction(fn, path)](creating-a-provider.md#joshprovider-findbyfunction-fn-path-promise-less-than-greater-than) ⇒ `Promise.<*>`
  * [.findByValue(path, value)](creating-a-provider.md#joshprovider-findbyvalue-path-value-promise-less-than-greater-than) ⇒ `Promise.<*>`
  * [.filterByFunction(fn, path)](creating-a-provider.md#joshprovider-filterbyfunction-fn-path-promise-less-than-object-greater-than) ⇒ `Promise.<Object>`
  * [.filterByValue(path, value)](creating-a-provider.md#joshprovider-filterbyvalue-path-value-promise-less-than-object-greater-than) ⇒ `Promise.<Object>`
  * [.mapByValue(path)](creating-a-provider.md#joshprovider-mapbyvalue-path-promise-less-than-array-less-than-string-greater-than-greater-than) ⇒ `Promise.<Array.<string>>`
  * [.mapByFunction(fn)](creating-a-provider.md#joshprovider-mapbyfunction-fn-promise-less-than-array-less-than-greater-than-greater-than) ⇒ `Promise.<Array.<*>>`
  * [.includes(key, path, val)](creating-a-provider.md#joshprovider-includes-key-path-val-promise-less-than-boolean-greater-than) ⇒ `Promise.<boolean>`
  * [.someByPath(path, value)](creating-a-provider.md#joshprovider-somebypath-path-value-promise-less-than-boolean-greater-than) ⇒ `Promise.<boolean>`
  * [.someByFunction(fn)](creating-a-provider.md#joshprovider-somebyfunction-fn-promise-less-than-boolean-greater-than) ⇒ `Promise.<boolean>`
  * [.everyByPath(path, value)](creating-a-provider.md#joshprovider-everybypath-path-value-promise-less-than-boolean-greater-than) ⇒ `Promise.<boolean>`
  * [.everyByFunction(fn)](creating-a-provider.md#joshprovider-everybyfunction-fn-promise-less-than-boolean-greater-than) ⇒ `Promise.<boolean>`
  * [.close()](creating-a-provider.md#joshprovider-close)
  * [.destroy()](creating-a-provider.md#joshprovider-destroy)
  * [.autoId()](creating-a-provider.md#joshprovider-autoid-promise-less-than-string-greater-than) ⇒ `Promise.<string>`
  * [.parseData(data)](creating-a-provider.md#joshprovider-parsedata-data) ⇒ `*`

### new JoshProvider(\[options])

| Param           | Type     | Description                                                                                                                   |
| --------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| \[options]      | `Object` | An object containing all the options required for your provider, as well as the ones provided by default with every provider. |
| \[options.name] | `string` | Required. The name of the table in which to save the data.                                                                    |

### joshProvider.init(Josh) ⇒ `Promise`

Internal method called on persistent Josh to load data from the underlying database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise` - Returns the defer promise to await the ready state.

| Param | Type  | Description                                             |
| ----- | ----- | ------------------------------------------------------- |
| Josh  | `Map` | In order to set data to the Josh, one must be provided. |

### joshProvider.get(key, path) ⇒ `Promise.<*>`

Retrieves a single value from the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<*>` - The data stored for the key, or at the path.

| Param | Type     | Description                                                                                                                                                                     |
| ----- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key   | `string` | The database key where the value is stored                                                                                                                                      |
| path  | `string` | Optional. Null if not provided by the user. The path within the key where the object is located. The path must support the same syntax as lodash does, for example: 'a\[0].b.c' |

### joshProvider.getAll() ⇒ `Promise.<Object.<*>>`

* Retrieves all values from the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Object.<*>>` - An object consisting of every key and value in the database. At the top level, the key is what the user providers when using set(key, value) and the value in the object is whatever's in the database. Every value should be parsed using `this.parseData()`\


### joshProvider.getMany(keys) ⇒ `Promise.<Object.<*>>`

Retrieves one or many values from the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Object.<*>>` - An object consisting every key requested by the user, and its value in the datbase. At the top level, the key is what the user providers when using set(key, value) and the value in the object is whatever's in the database. Every value should be parsed using `this.parseData()`

| Param | Type             | Description                                   |
| ----- | ---------------- | --------------------------------------------- |
| keys  | `Array.<string>` | A list of keys to retrieve from the database. |

### joshProvider.random(count) ⇒ `Promise.<Object.<*>>`

Retrieves one or more random values from the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Object.<*>>` - An object representing one or more random keys taken from the database, with their values. At the top level, the key is what the user providers when using set(key, value) and the value in the object is whatever's in the database. Every value should be parsed using `this.parseData()`

| Param | Type     | Default | Description                                                                      |
| ----- | -------- | ------- | -------------------------------------------------------------------------------- |
| count | `Number` | `1`     | An integer representing the number of random values to obtain from the database. |

### joshProvider.randomKey(count) ⇒ `Promise.<Array.<string>>`

Retrieves a random key from all the database keys for this Josh.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Array.<string>>` - An array of random keys taken from the database, or a single key if count is 1.

| Param | Type     | Default | Description                                                                    |
| ----- | -------- | ------- | ------------------------------------------------------------------------------ |
| count | `Number` | `1`     | An integer representing the number of random keys to obtain from the database. |

### joshProvider.has(key, path) ⇒ `Promise.<boolean>`

Verifies whether a key, or value at path, exists in the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<boolean>` - Whether the key (or value at path) exists.

| Param | Type     | Description                                                                                                                          |
| ----- | -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| key   | `string` | The key of which the existence should be checked.                                                                                    |
| path  | `string` | Optional. Null if not provided by the user. If provided, should return whether a value exists at that path, assuming the key exists. |

### joshProvider.keys() ⇒ `Promise.<Array.<string>>`

Retrieves all the indexes (keys) in the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Array.<string>>` - Array of all indexes (keys) in the database.\


### joshProvider.values() ⇒ `Promise.<array.<*>>`

Retrieves all of the values in the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\


### joshProvider.count() ⇒ `Promise.<integer>`

Retrieves the number of rows in the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<integer>` - The number of rows in the database.\


### joshProvider.set(key, path, val) ⇒ `Promise.<Provider>`

Saves a key in the database, along with its value.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Provider>` - This provider.

| Param | Type     | Description                                                                                                                       |
| ----- | -------- | --------------------------------------------------------------------------------------------------------------------------------- |
| key   | `string` | The name of the key. If the key already exists, the value should be overriden.                                                    |
| path  | `string` | Optional. Null if not provided by the user. Defines where, in an object or array value, to place the provided data.               |
| val   | `*`      | The data to write in the database for the key, or at the path for this key. This value MUST be written using serialize-javascript |

### joshProvider.setMany(data, overwrite) ⇒ `Promise.<Provider>`

Writes many different keys and their values to the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Provider>` - This provider.

| Param     | Type      | Description                                                                                                                                                                                                             |
| --------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data      | `Object`  | The data to write to the database. Should be an object where each property is a key and its value is the value to write. Does not support writing with paths. Format is: `json {   key1: 'value1',   key2: 'value2', }` |
| overwrite | `boolean` | Whether to overwrite existing keys provided in the incoming data.                                                                                                                                                       |

### joshProvider.delete(key, path) ⇒ `Promise.<Provider>`

Deletes a key and its value, or the part of an object or array value, from the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Provider>` - This provider.

| Param | Type     | Description                                                                                                                                     |
| ----- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| key   | `string` | The name of the key to remove, or _from_ which value to remove data at the path.                                                                |
| path  | `string` | Optional. Null if not provided by the user. The path that should be deleted, if one is provided. Ideally, this could use `unset()` from lodash. |

### joshProvider.clear() ⇒ `Promise.<Provider>`

Deletes every single entry in the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Provider>` - This provider.\


### joshProvider.push(key, path, value, allowDupes) ⇒ `Promise.<Provider>`

Pushes a new value into an array stored in the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Provider>` - This provider.

| Param      | Type      | Description                                                                                                               |
| ---------- | --------- | ------------------------------------------------------------------------------------------------------------------------- |
| key        | `string`  | The key where to push a new value. The key's value must be an array (unless a path is used, then it should be an object). |
| path       | `string`  | Optional. Null if not provided by the user. If provided, the value at that path should be an array.                       |
| value      | `*`       | The value to push into the array.                                                                                         |
| allowDupes | `boolean` | Whether to allow duplicates to be pushed into the array. If true, should not ... well... allow duplicates.                |

### joshProvider.remove(key, path, val) ⇒ `Promise.<Provider>`

Removes a value from an array stored in the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Provider>` - This provider.

| Param | Type              | Description                                                                                                        |
| ----- | ----------------- | ------------------------------------------------------------------------------------------------------------------ |
| key   | `string`          | The key where to remove a value from. The key's value must be an array (unless a path is used).                    |
| path  | `string`          | Optional. Null if not provided by the user. If provider, the value at that path should be an array.                |
| val   | `*` \| `function` | The value to remove from the array, or a function provided by the user to remove from the array (using findIndex). |

### joshProvider.inc(key, path) ⇒ `Promise.<Provider>`

Increments a numerical value within the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Provider>` - This provider.

| Param | Type     | Description                                                                                             |
| ----- | -------- | ------------------------------------------------------------------------------------------------------- |
| key   | `string` | The key to increment. The value must be a Number.                                                       |
| path  | `string` | Optional. Null if not provided by the user. If provided, the value at that path must be a Number value. |

### joshProvider.dec(key, path) ⇒ `Promise.<Provider>`

Decrements a numerical value within the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Provider>` - This provider.

| Param | Type     | Description                                                                                             |
| ----- | -------- | ------------------------------------------------------------------------------------------------------- |
| key   | `string` | The key to decrement. The value must be a Number.                                                       |
| path  | `string` | Optional. Null if not provided by the user. If provided, the value at that path must be a Number value. |

### joshProvider.math(key, path, operation, operand) ⇒ `Promise.<Provider>`

Executes a mathematical operation on a numerical value within the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Provider>` - This provider.

| Param     | Type     | Description                                                                                            |
| --------- | -------- | ------------------------------------------------------------------------------------------------------ |
| key       | `string` | The key where the operation should be executed. The value must be a Number value.                      |
| path      | `string` | Optional. Null if not provided by the user. If provided, the value at the path must be a Number value. |
| operation | `string` | One of the supported operations (listed in this function).                                             |
| operand   | `Number` | The secondary Number for the mathematical operation.                                                   |

### joshProvider.findByFunction(fn, path) ⇒ `Promise.<*>`

Finds and returns a value using a function.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<*>` - The first value found by the function, or `null` if no value found.

| Param | Type       | Description                                                                                                                                                                                                                                                              |
| ----- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| fn    | `function` | A function to execute on every value in the database. This function should provide both the `value` and `key` as arguments and will return a boolean. findByFunction should support asynchronous functions (the `fn` return could be a promise that requires resolution) |
| path  | `string`   | Optional. If provided, the function should be provided the value at the path rather than at the root.                                                                                                                                                                    |

### joshProvider.findByValue(path, value) ⇒ `Promise.<*>`

Finds and returns an entire value, by checking whether a specific sub-value was found a the given path.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<*>` - The first value found, or `null` if no value found.

| Param | Type     | Description                                     |
| ----- | -------- | ----------------------------------------------- |
| path  | `string` | The path where to check if the value is present |
| value | `*`      | The value to check for equality.                |

### joshProvider.filterByFunction(fn, path) ⇒ `Promise.<Object>`

Finds and returns one or more values using a function to check whether the value is desired.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Object>` - The values found by the function, or `{}` if no value found.

| Param | Type       | Description                                                                                                                                                                                                                                                                    |
| ----- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| fn    | `function` | A function to execute on every value in the database. This function should be provided both the `value` and `key` as arguments and will return a boolean. filterByFunction should support asynchronous functions (the `fn` return could be a promise that requires resolution) |
| path  | `string`   | The path where to check if the value is present                                                                                                                                                                                                                                |

### joshProvider.filterByValue(path, value) ⇒ `Promise.<Object>`

Finds and returns one or move value, by checking whether a specific sub-value was found at the given path.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Object>` - The values found by this function, or `{}` if no value found.

| Param | Type     | Description                                     |
| ----- | -------- | ----------------------------------------------- |
| path  | `string` | The path where to check if the value is present |
| value | `*`      | The value to check for equality.                |

### joshProvider.mapByValue(path) ⇒ `Promise.<Array.<string>>`

Retrieves the value at the specified path for every stored object or array in the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Array.<string>>` - An array of the values at that path

| Param | Type     | Description                    |
| ----- | -------- | ------------------------------ |
| path  | `string` | The path to get the data from. |

### joshProvider.mapByFunction(fn) ⇒ `Promise.<Array.<*>>`

Runs a function for every value in the database and returns an array with the return of that function for each value.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<Array.<*>>` - An array of the values returned by the function for each value.

| Param | Type       | Description                                                                                                                                                                                                                   |
| ----- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fn    | `function` | The function should be provided the `key` and `value` as arguments (in that order) and will return a value. mapByFunction should support asynchronous functions (the `fn` return could be a promise that requires resolution) |

### joshProvider.includes(key, path, val) ⇒ `Promise.<boolean>`

Verifies if a value is part of an array at the key (or the path within that key).

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<boolean>` - Whether the value is in the array.

| Param | Type     | Description                                                                                       |
| ----- | -------- | ------------------------------------------------------------------------------------------------- |
| key   | `string` | The key in which to verify the existence of the value. Should be an array, unless a path is used. |
| path  | `string` | Optional. Null if not provided by the user. Value at this path is expected to be an array.        |
| val   | `*`      | The value to check in the array.                                                                  |

### joshProvider.someByPath(path, value) ⇒ `Promise.<boolean>`

Verifies if the provided value is located in _any_ of the values stored in the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<boolean>` - Should return true as soon as the value is found, or false if it hasn't been.

| Param | Type     | Description                                                                                                                |
| ----- | -------- | -------------------------------------------------------------------------------------------------------------------------- |
| path  | `string` | Optional. Null if not provided by the user. If provided, the value would need to be equal to the data stored at that path. |
| value | `*`      | The value to check for at that path.                                                                                       |

### joshProvider.someByFunction(fn) ⇒ `Promise.<boolean>`

Verifies if something is true in any of the values stored in the database, through a function.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<boolean>` - Whether the `fn` has returned true for any value.

| Param | Type       | Description                                                                                                                                                                                                                                                                                                                                         |
| ----- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fn    | `function` | The function should be provided both the `value` and `key` for each entry in the database, and will return a boolean. someByFunction is expected to return `true` immediately on the first occurence of the `fn` returning true. someByFunction should support asynchronous functions (the `fn` return could be a promise that requires resolution) |

### joshProvider.everyByPath(path, value) ⇒ `Promise.<boolean>`

Verifies if a value at a path is identical to the one provided, for every single value stored in the database.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<boolean>` - Whether the value was equal to the one at the path for every single value in the database.

| Param | Type     | Description                                                 |
| ----- | -------- | ----------------------------------------------------------- |
| path  | `string` | The path where the value should be checked.                 |
| value | `*`      | The value that should be checked for equality at that path. |

### joshProvider.everyByFunction(fn) ⇒ `Promise.<boolean>`

Verifies if a condition is true on every single value stored in the database, using a function.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<boolean>` - Whether the `fn` has returned true for every value.

| Param | Type       | Description                                                                                                                                                                                                                               |
| ----- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fn    | `function` | The function should be provided botht he `value` and `key` for each entry in the database, and will return a boolean. everyByFunction should support asynchronous functions (the `fn` return could be a promise that requires resolution) |

### joshProvider.close()

Closes the database. This function should be used to shut down any connection or file access to the database this provider refers to.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\


### joshProvider.destroy()

Deletes the database. This function should delete everything in the specific table used by this database (for the josh's **name** specifically) It should also remove any temporary table, as well as the "autoid" saved for it. After this method is run, no trace of the specific josh should exist.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\


### joshProvider.autoId() ⇒ `Promise.<string>`

Returns the "next" automatic ID for this josh. AutoId should be a string, and can technically be anything you want - either a numerically incremented value or just an automatic row ID or DB ID (autonum, mongo's \_id , etc). No 2 Ids should ever be identical.

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `Promise.<string>` - An automatic ID.\


### joshProvider.parseData(data) ⇒ `*`

Internal method to read data from the database. This is essentially the contrary of `serialize-javascript`'s "serialize()" method. Note: EVAL IS NORMAL. As long as 100% of the data you read from this has been written by serialize(), this is SAFE. If you have any doubts as to what data has been written, or if you have to deal with mixed or unsafe data, then you should take further action to ensure you are not subject to security breaches!

**Kind**: instance method of [`JoshProvider`](creating-a-provider.md#joshprovider)\
**Returns**: `*` - A value parsed through eval, which will be valid javascript.

| Param | Type     | Description                                            |
| ----- | -------- | ------------------------------------------------------ |
| data  | `string` | A string ("JSON") generated by `serialize-javascript`. |
