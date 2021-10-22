---
description: How to install the JOSH Core Database Wrapper
---

# Installation

JOSH is installed very simply through `yarn` or `npm`:&#x20;

```
npm i @joshdb/core
* OR *
yarn add @joshdb/core
```

JOSH itself has very little dependencies, specifically it only depends on lodash which is installed automatically when you install @joshdb/core.

### Provider Dependency

However, JOSH cannot function without a [Provider](../providers/about.md), which provides the communication layer between @joshdb/core and the database you're storing data in. Every provider may have its own specific pre-requisites and sub-dependency, so please take care to read the page for the provider you intend to use.

### What's next?

See the Providers page and choose one!

{% content-ref url="../providers/about.md" %}
[about.md](../providers/about.md)
{% endcontent-ref %}

