---
description: >-
  JOSH is the JavaScript Object Storage Helper - a simple, effective, and
  efficient database wrapper.
---

# Welcome to JOSH

![Credits: See bottom of page](.gitbook/assets/JOSH\_p\_light.svg)

JOSH is the JavaScript Object Storage Helper - a simple, effective, and efficient database wrapper. The idea of JOSH came out of my existing wrapper, Enmap, which suffers from two very unique but important flaws:

* It cannot scale very well, being locked to better-sqlite3 which doesn't support live data updates
* It requires the use of a cache, since most of its features, as used by most people, require the cache to be available.

JOSH intends to solve both those problems that can't actually be resolved in Enmap itself, by moving away from the synchronous nature of better-sqlite3 and using [Promises](https://js.evie.dev/promises). In this way, JOSH can keep most of Enmap's features but add on a whole lot more.

Now that this history lesson is done, what exactly _is_ JOSH except being a contrast to something I've already done?

JOSH is a promise-based database wrapper that assists in quick prototyping and rapid development of Node.js applications that require data storage. It aims at removing some of the complexity of database management and communication by providing a _simple_ interface that anyone can pick up and use.

JOSH can communicate with many different database systems through the use of _Providers_, which are a translation layer between the JOSH API and the Database system.

JOSH is _not an ORM_ , in the sense that it does not handle either models or relationships. In fact, I personally do not like ORMs at all due to their inherent complexity, so don't expect those features here!

_Logo Credits: _[_CyaCal _](https://github.com/cal3432)_and _[_GlitchyPSIX_](https://github.com/GlitchyPSIX)__
