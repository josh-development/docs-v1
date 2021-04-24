---
description: >-
  A provider that Josh can use to communicate with an HTTPS API, on a remove
  server running the josh-api server
---

# HTTPS

### Running the installer

In your project folder, you should be able to install using this command:

```
npm i @joshdb/https
** OR **
yarn add @joshdb/https
```

## Usage

Using the JSON provider goes as such:

```js
const Josh = require('josh');
const JoshHTTPS = require('@joshdb/https');

const db = new Josh({
  name: 'testing',
  provider: JoshHTTPS,
  // See below for all provider options.
  providerOptions: {},
});

db.defer.then(async () => {
  console.log(`Connected, there are ${await db.size} rows in the database.`);
});
```

## Provider Options

Here is a list of full options this provider supports:

| Param                          | Type                 | Description                                                             |
| ------------------------------ | -------------------- | ----------------------------------------------------------------------- |
| [providerOptions]              | <code>Object</code>  | The Provider Options Object, with the below properties:                 |
| [providerOptions.name]         | <code>string</code>  | someone please update it, idk what's this                               |
| [providerOptions.apiKey]       | <code>string</code>  | someone please update it, idk what's this                               |
| [providerOptions.url]          | <code>string</code>  | someone please update it, idk what's this                               |
