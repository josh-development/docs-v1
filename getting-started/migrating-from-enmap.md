---
description: >-
  Here we describe how to transfer your data from an Enmap instance, and what
  code changes you'll have to make in your code for Josh to work.
---

# Migrating from Enmap

While Josh and Enmap are based on the same basic concepts and ideas, there are some changes that will need to happen in your code if you want to move from Enmap to Josh. 

A few decisions I made here and there mean that unfortunately, almost all lines related to your database interactions will need to be changed one way or another, so before we start, I apologize from the bottom of my heart that this isn't as straightforward as "change a few lines and import the data". The significant work you'll have to do to convert is entirely my fault, so make sure that you _need_ to move to Josh before you start, otherwise, you're just adding pain onto yourself and I can't take all the blame for that.

## Why Migrate?

First off: you shouldn't just migrate from Enmap to Josh "just because Josh is newer". Josh isn't an _upgrade_ to Enmap, it's a different module altogether which offers only a few very clear benefit and two downsides that might not be worth it for you. 

The first reason why you _should_ migrate, is if you need to access your data from more than one process. For example, if you need to shard a discord.js bot, or if you want a dashboard separated from the bot itself. Or, if you simply have more than one app accessing the same database. Since Enmap doesn't do that \(well, it "does" with polling but it's pretty crappy at it\), going to Josh is a valid solution.

The second reason you'd want to migrate is if you want to move away from SQLite and want a database server that's more powerful or hosted remotely. Josh offers various providers that give you this capability.

## Before you migrate

So before you get into this, I would very strongly recommend you get very comfortable with the use of promises. Thing is, where Enmap doesn't use promises at all except for the defer option \(which you usually don't need except for specific circumstances\), Josh is quite the contrary: _Everything Is Promises_. So, if you don't understand async/await or how to resolve promises you're going to have a bad time. 

[The Promise page on my JS guide](https://js.evie.dev/promises) should cover most of the concepts required for you to use Josh so go through that page and then come back. I suggest using async/await whenever possible, and that's how I build all my examples and documentation.

_**MAKE A BACKUP OF YOUR PROJECT NOW**_. If you're using GIT that's simple, just make sure all your changes are commited. If not, just create a zip file or a copy of your project folder \(it'll take time unless you delete node\_modules first\).

## Step 1: Installation

The TL;DR of the Installation page is that you just need to run `npm i josh@latest` or `yarn add josh@latest` in your project to get Josh itself. You can simply do this in your project folder, because we can do all this within that folder without losing any data. 

Then, you choose a provider and you install that, too, with its pre-requisites. In this example we're going for the SQLite provider, but the instructions should be identical for all of them except for the provider name. So in our case, with the windows-build-tools already installed \(because you're using Enmap, you have those already!\) we can just `npm i @josh-providers/sqlite` or `yarn add @josh-providers@sqlite` to add it. 

With those 2 modules added we can continue on to the migration itself. DO NOT DELETE OR UNINSTALL ENMAP OR ITS DATA YET, obviously.

## Step 2: Migration

The magic part of this is that Josh can import Enmap's exported data directly. That is to say, we're going to use the export\(\) method from Enmap to get all of its data, and we're going to use the import\(\) method in Josh to insert it. There's no loop or complicated code required here, it's pretty much just a string we shove between the two.

Create a new file in your project called `migration.js`. In this file we're going to add the code to transfer the data. Here it is, with comments to help you understand what it does.

```javascript
// Require enmap, josh, and the provider
const Enmap = require("enmap");
const Josh = require("@joshdb/core");
const provider = require("@joshdb/sqlite");

// Initialize the enmap. You MUST of course use the same NAME option,
// and if you've changed the dataDir option, set it identically here too.
// However, we must make sure to fetchAll here.
const source = new Enmap({
  name: "settings",
  fetchAll: true,
});

// Initialize Josh. Probably easier to keep the same name for the table,
// for your convenience.
const target = new Josh({
  name: "settings",
  provider,
});

// We need to await the enmap's initialization and data loading,
// so we're going to do that with an async IIFE to simplify things.
// An IIFE is just a function that runs immediately, in this case an async one.
(async () => {
  await source.defer;
  console.log(`Loaded Enmap with ${source.count} rows to transfer`);
  console.log(`Target JOSH currently has ${await target.size} rows.`);
  
  // Get the exported data from Enmap:
  const data = source.export();
  
  // Import it into Josh:
  await target.import(data);
  
  console.log(`Migration done! Target JOSH now has ${await target.size} rows!`);
})();
```

Now that the data is completely migrated, we're ready to move on. To verify that the data is all there, you'll need to open the target database and look in it, if you don't trust the number displayed in the last console.log. This is done through some sort of database management interface, for SQLite you can use "DB Browser for SQLite" and open the ./data/josh.sqlite file. For other providers, it will depend on where it's stored.

## Step 3: Changing your Code

Now comes the hard part. You'll need to change your entire code for Josh. This includes every single line where you're getting, setting, or modifying the database. But, there are some general guidelines that will clarify exactly what changes need to be made. 

The Initialization

This is an easy one: the initialization for Josh is exactly what you used above in the migration script. You import Josh, the Provider, then you initialize it with the new Josh\(\) line. 

> There is currently no multi\(\) method in Josh, this is in the works, though! For now each instance must be initialized separately.

### The Key/Path system

In Josh, there is no separate "key" and "path" when it comes to arguments. Basically I realized that with the various arguments between functions, it sometimes was vague or confusing what went where. To simplify this, it's now a single argument that starts each method where a key and/or path is necessary. 

So, the new system works as a single string, where each part is separated by a dot to indicate a level in the object. Let's see an example with set\(\) first, to, errr, "set the table" as it were. 

```javascript
// In Enmap, you did this: 
enmap.set("somekey", { a: 1, b: 2, c: 3 });
// And then setting a prop was like this: 
enmap.set("somekey", 4, "d");

// In Josh, the equivalent is the same for a top-level value:
await josh.set("somekey", { a: 1, b: 2, c: 3 });
// But setting inside an object is like this: 
await josh.set("somekey.d", 4);
// And overriding is the same
await josh.set("somekey.a", "one");
```

If you need to access a property that's nested in another level, you can just chain the path exactly as you would have in Enmap, so `await josh.set("somekey.a.foo.bar", "newvalue")` would set at the 3rd level of the object.

Every other method will have the same tweak, from push\(\) and remove\(\) in arrays to get\(\) and has\(\) and all these wonderful things. 

{% hint style="info" %}
Since the key/path is a string you can use template literals for variables. For example, in a per-server settings context:

```javascript
await client.settings.get(`${message.guild.id}.disabledCommands`);
```
{% endhint %}

### Find, Filter and other loops

Because Josh is not cached in memory, there are a few little changes to the way array methods work. First and foremost it's important to know that for most providers, using the looping methods will cause a significant increase in temporary memory usage \(because data still needs to be loaded in memory to be processed in most cases\), and using a _path_ rather than a function is going to always be much faster and efficient. In fact, for providers supporting JSON data types \(rethink, mongo, postgresql\), using path equality means no data is loaded in memory, it's all database-processed and is faster by an order of magnitude. 

{% hint style="info" %}
Josh support async functions for find\(\), filter\(\) and some\(\). However, they will be slower due to "whatever async thing you're doing".
{% endhint %}

```javascript
// Get a value by path: where the <value>.users.owner is the current user,
// basically "a guild where I'm owner that has settings" if that makes sense.
const myGuild = client.settings.find("users.owner", message.author.id);

// Filter to get all users in the database where the permissions.admin is true
const admins = blogUsers.filter("permissions.admin", true);

// The 2 above, in function equivalence:
const myGuild = client.settings.find( set => set.users.owner = message.author.id);
const admins = blogUsers.filter(user => user.permissions.admin);
```

Also note that _the return value_ for these functions has changed. Rather than having `find()` and `findKey()` separated, each method that can return multiple results will always return an array of \[key, value\] pairs, such as `[ [a, 1], [b, 2], [c, 3] ]`. This is the case even if you're using a path check.

And again, I must insist on the fact that doing a path check is _much more efficient_, even if it can only be done with an equal check for the moment \(should change later\).

### Methods that have changed names

Here is a list of methods and properties that have changed in either their name, or usage.

* autonum =&gt; `await josh.autoId()`
* size, count =&gt; combined as `await josh.size;`
* deleteAll\(\) =&gt; `await josh.delete(josh.all);`
* array\(\), values =&gt; `await josh.getMany(josh.all);`
* keyArray\(\), indexes =&gt; combined as `await josh.keys();`
* findAll\(\) =&gt; use filter\(\) instead, same thing.
* findKey\(\) =&gt; use find\(\) and it returns the key, too.
* exists\(\) =&gt; `await josh.has("key.path");`

### Methods that are not yet implemented

Josh being in early access right now, the following are not implemented yet:

* observe\(\)

### Methods that will not be implemented

A lot of things in Enmap were there due to the initial implementation being heavily tied to either being a Map extension, or being derived from Discord.js Collections. These will not be implemented in Enmap as they are either of little use, or being doable with some other methods:

* fetch/fetchEverything: Not required, no longer relevant.
* evict: Not required, no longer relevant.
* changed: Cannot be implemented.
* sweep, partition, clone, equals: Did anyone, in the history of Enmap, ever use those???
* setProp, pushIn, getProp, deleteProp, removeFrom, hasProp: They're deprecated, and can all be done with the simple key/path system.
* filterArray: Already returning an array, this is unnecessary.



Conclusion

So yes, I get that this is a pretty hefty page, with a lot of things to check and change. But if you really _did_ need it, at least now you're done!

{% hint style="danger" %}
Don't forget to TEST EVERYTHING before uninstalling enmap, better-sqlite3, and deleting the enmap.sqlite file \(you might also want to keep that one just in case\).
{% endhint %}

