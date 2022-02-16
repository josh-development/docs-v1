---
description: Frequently Asked Questions about JOSH and its providers
---

# FAQ

## Is JOSH better than [Enmap](https://enmap.evie.dev)?

Not really. While JOSH does have some features Enmap doesn't (such as providers, for example), and can be used on more hosts due to that (like Heroku), it's not "better", just different. Enmap still has the advantage in simplicity since it doesn't use promises. It's also more mature and stable, whereas JOSH is still a bit young.

## When should I consider migrating away from JOSH?

There's a few indications that maybe you'd want to move away from this system.

One of them is if you need more control over the data and how it's stored. JOSH just throws anything you give it into a database, it makes no effort to check, type, or validate that data.

Another is if you require modelling ("models") or types for your data, as in, very specific limitations on what data can be stored. I've no intention of adding these features.

If you find that you're often pulling data from JOSH and manually manipulating it, or if you're making extensive use of the serializer/deserializer feature, maybe it's time to move.

## Are you ever going to add Types or Typescript support?

No. While there are typing files in JOSH, those are all provided by some of my users which contribute to the success of the project with their dedication to TypeScript but... I have no intention, personally, of managing types. However, the community has obliged, there's a [Typescript Example](../examples/typescript-usage.md), and I will accept PRs meant to enhance the experience of TS users.

As for adding types to the stored data...  I won't, ever, it's not happening. JOSH isn't a typed ORM, it's the antitheses of typed ORMs. It's the typed ORM's worse nightmare, because I make every effort **not** to type and create models. The entire point of JOSH is to be freeform "whatever you want stored it stores it" concept. JOSH is not compatible with the typed data philosophy at all and will never be.
