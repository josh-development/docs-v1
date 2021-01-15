# Testing Stuff

If you feel the need to "test" JOSH's functionality from a command line, you're not alone, because I do to! That's why I created a very simple script that lets me directly import and interact with JOSH from the command line. That way I can set, get, delete, and do all the things without having to restart a script every time. 

The script uses a simple `readline` module that's core to node, so really the only thing it needs to run is `josh` itself, and a provider such as `@josh-providers/sqlite` . 

You'll need to install the appropriate provider, see [Providers ](../providers/about.md)for instructions.

Here's the script: 

```javascript
const readline = require('readline');
const Josh = require('@joshdb/core');
const provider = require('@joshdb/sqlite');

const clean = async (text) => {
  if (text && text.constructor.name == 'Promise') {
    text = await text;
  }
  if (typeof evaled !== 'string') {
    text = require('util').inspect(text, { depth: 1 });
  }
  return text;
};

const evalCode = async (code) => {
  try {
    const evaled = eval(code);
    return await clean(evaled);
  } catch (err) {
    return await clean(err);
  }
};

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

const db = new Josh({
  name: 'testing',
  provider,
});

(async () => {
  console.log(`Connected, there are ${await db.size} rows in the database.`);
})();

rl.on('line', async (input) => {
  console.log(`PROCESSING INPUT: ${input}`);
  const result = await evalCode(input);
  console.log(result);
});

```

Once it runs, you can just type away directly in the command line! For example, `db.set("test", "test")` just adds that key/value pair, as you'd expect.

Have fun!

