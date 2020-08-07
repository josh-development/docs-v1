---
description: >-
  JOSH can use multiple different providers to communicate with as many
  databases. While providers are currently limited, they will be added over
  development time.
---

# Providers

In order to save data to a database, Josh uses a secondary layer of code called a _Provider_. This provider receives specific instructions from Josh and uses those instructions to communicate with the database. So Josh itself doesn't need to know how the database works, it only needs to know how the Provider works, and since every provider has the exact same API \(its communication protocol\), any provider that adheres to that protocol can be used.

### Official Providers

I provide a few common/popular providers. These are all fully tested and any change I make to Josh will reflect in the providers simultaneously. Any issue with these providers should be reported on Github or through my Discord. 

Installing official providers is done through the `@josh-providers` scope. This is helpful to identify them - if it's not installed from this, it's not mine!

Available official providers: 

* [sqlite ](sqlite.md): Uses better-sqlite3, stored on disk as a single file.
* [mongo ](mongo.md): _**UNDER DEVELOPMENT**_  Uses mongo, stored on a mongodb server.
* [postgre ](postgre.md): _**UNDER DEVELOPMENT**_ Stores data in a postgresql database using the pg module.
* [https ](https.md): _**UNDER DEVELOPMENT**_ Communicates with a secure SSL HTTP server to store data remotely.

### Unofficial Providers

Josh being early access, no providers have been submitted for this list.

\[ TBD : Documentation for how Providers should work, what methods are required, etc \]

