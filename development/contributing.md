---
description: Want to contribute to Josh's development? Please read this page!
---

# Contributing

I love coding, but sometimes, managing multiple projects can be a tough job. I welcome the contributions of the community to make the experience of using JOSH better. 

### What can you contribute?

You, as a developer, have a few things you can contribute to. The Core wrapper, any of the existing Providers, a new Provider of your own making... and maybe typings for any of these. Also some future projects related to JOSH. See the list below.

### The JOSH Core Wrapper

The Wrapper, aka @joshdb/core , is obviously the most important part since it's what the JOSH user interacts with. It contains all the methods that controls the providers, which in turn interact with the database. As such, it's a great abstraction layer meant to simplify interaction and code.

To contribute to the Core, please see [the github repository](https://github.com/eslachance/josh), and open a PR to this repo.

### The Providers

Providers are the layer of communication between the Core and the Databases. All officially supported providers are located on a separate github repository. You can directly create new PRs to this repository to modify existing providers or create a new one. See [Creating a Provider](creating-a-provider.md) for more details.

### The HTTPS Provider and Server

This started off as a pretty secret thing I wanted to do, but, it's become apparent it's a bit much for me. So let me lay it out for you. The plan is to provide and HTTPS provider which connects to a specially built server that hold both the database as well as a significant amount of JavaScript processing. And therein lies the crux of the issue. Since some features of JOSH support JavaScript functions, it means that providers must be able to run what is essentially arbitrary user code. Also directly using eval\(\) to read data, so, obviously, that's bad.

This isn't an issue when you're running any other provider since it's on your own PC, your own database setup, etc... but if I'm going to be running an HTTPS server that has the ability to parse and run user code, a seriously _solid_ security-oriented setup must be created. So, if you know a fair amount about the possibility of running a dockerized safe eval\(\) for arbitrary user-provided javascript on a nodejs based server, please join my discord \(link at the top of this page\) and talk to me!

