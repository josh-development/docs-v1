---
description: >-
  JOSH can use multiple different providers to communicate with as many
  databases. While providers are currently limited, they will be added over
  development time.
---

# About Providers

## What is a Provider?

A Provider is a layer of communication between Josh, and a database. Each provider has a precise set of instructions it can receive from Josh, where each instruction tells it what to do in the database.

## What Providers are available?

At the moment, the only provider that's functional is [sqlite](sqlite.md). As I continue developing, I'll be adding more providers to the list - see the list on the left in the Table of Content to see which ones I'm working on!

## Can I add my own Provider?

You sure can! Even though I do my best to create providers for popular storage systems, I can't possibly create all of them. If you have a storage system you'd like to use, by all means you can go about [Creating a Provider](../development/creating-a-provider.md).

> Official providers are always available under the `@josh-providers/` scope. Only official providers are supported officially, and are guaranteed functional and safe. Install third-party providers at your own risks!

## How do I use a Provider?

Providers must be installed separately from Josh and are installed as any NPM module is, through either `yarn` or `npm` in the command line. For example, `yarn add @josh-providers/sqlite`. Note that each provider may have pre-requisites before installation, check the provider page for details.

To use a provider, simply require it, give it to Josh along with the `providerOptions` if required, and Josh does the rest!

For example, again with the sqlite module:

```javascript
const Josh = require("josh");
const provider = require("@josh-providers/sqlite");

const myDb = new Josh({
  name: 'test',
  provider,
  providerOptions: {
    dataDir: './data'
  }
});
```

