# sqlite

SQLite communication is provided by better-sqlite3. 

This provider requires building better-sqlite3 from source, so you'll need to make sure your system is ready for that.

### Pre-Requisites

{% tabs %}
{% tab title="Windows" %}
On Windows, two things are required to install better-sqlite3. Python 2 or 3, and the Visual Studio C++ Build Tools. They are required for any module that is _built_ on the system, which includes sqlite.

To install the necessary prerequisites on Windows, the easiest is to simply run the following commands, _under an **administrative** command prompt or powershell:_

```javascript
npm i -g --add-python-to-path --vs2015 --production windows-build-tools

npm i -g node-gyp
```

> It's _very important_ that this be run in the **administrative** prompt, and not a regular one.

Once the windows-build-tools are installed \(this might take quite some time, depending on your internet connection\), **close all open command prompts, powershell windows, and editors with a built-in console/prompt**. Otherwise, the next command will not work.
{% endtab %}

{% tab title="Linux" %}
On Linux, the pre-requisites are much simpler in a way. A lot of modern systems \(such as Ubuntu, since 16.04\) already come with python pre-installed. For some other systems, you might have to fiddle with it to either get python installed, or working. Google will be your friend.

Check if it's installed by running `python --version` which should return the appropriate 2.x or 3.x version.

As for the C++ build tools, that's installed using the simple command: `sudo apt-get install build-essential` for most debian-based systems. For others, look towards your package manager and specifically "GCC build tools". Your mileage may vary but hey, you're using Linux, you should know this stuff.
{% endtab %}
{% endtabs %}

### Installation

In your project folder, assuming the above pre-requisites are followed, you should be able to just install using this command:

```text
npm i @josh-providers/sqlite
** OR **
yarn add @josh-providers/sqlite
```

### Usage

Using the sqlite provider goes as such:

```javascript
const Josh = require('josh');

const db = new Josh({
  name: 'testing',
  provider: '@josh-providers/sqlite',
});

db.defer.then( () => {
  console.log(`Connected, there are ${db.count} rows in the database.`);
});
```

