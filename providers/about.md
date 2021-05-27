---
description: >-
  JOSH can use multiple different providers to communicate with as many
  databases. While providers are currently limited, they will be added over
  development time.
---

# Providers

## What is a Provider?

A Provider is a layer of communication between JOSH, and a database. Each provider has a precise set of instructions it can receive from JOSH, where each instruction tells it what to do in the database.

## What Providers are available?

At the moment, only a few providers are available at all. As time develops, more will be added. Please see the menu on the left to see available providers!

## Can I add my own Provider?

You sure can! Even though I do my best to create providers for popular storage systems, I can't possibly create all of them. If you have a storage system you'd like to use, by all means you can go about [Creating a Provider](../development/creating-a-provider.md).

> Official providers are always available under the `@joshdb/` scope. Only official providers are supported officially, and are guaranteed functional and safe. Install third-party providers at your own risks!

## How do I use a Provider?

Providers must be installed separately from Josh and are installed as any NPM module is, through either `yarn` or `npm` in the command line. For example, `yarn add @joshdb/sqlite`. Note that each provider may have pre-requisites before installation, check the provider page for details.

To use a provider, simply require it, give it to Josh along with the `providerOptions` if required, and Josh does the rest!

For example, again with the sqlite module:

```javascript
const Josh = require("@joshdb/core");
const provider = require("@joshdb/sqlite");

const myDb = new Josh({
  name: 'test',
  provider,
  providerOptions: {
    dataDir: './data'
  }
});
```

