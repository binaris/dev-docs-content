---
title: DB Admin Tool
route: db-admin-tool
description: 'How to use the DB Admin Tool'
category: 'Main Concepts'
priority: 25
---

> Note: Your Reshuffle packages need to have the following minimum dependencies to utilize DB Admin Tool functionality: 

```json
"@reshuffle/local-proxy": "^0.3.4",
"@reshuffle/db-admin": "0.0.10",
"@reshuffle/server-function": "^0.2.2"
```

# DB Admin Tool

We value being able to add, edit and even delete entries from a database on the fly. Our DB Admin Tool will make modifying data a piece of cake.

### What is the DB Admin Tool?

DB Admin Tool is a basic middleware for express which makes it possible to view your DB in the browser for any Reshuffle app.

## Adding DB Admin Tool to your project

Reshuffle provides an easy way to add the DB Admin Tool to any express app ensuring that it works right out of the box. Before you can start using it, youll need to install only one dependency [@reshuffle/db-admin](https://www.npmjs.com/package/@reshuffle/db-admin) via npm:

```bash
npm install @reshuffle/db-admin
```

Next, import the DB admin package and express:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">backend/_handler.js ↓</span></div>

```js
import express from 'express';
import devDBAdmin from '@reshuffle/db-admin';

const app = express();
```

After you declare the express app, add this line:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">backend/_handler.js ↓</span></div>

```js
app.use("/dev/db-admin", express.json(), devDBAdmin.devDBAdminHandler);
```

It should look something like this:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">backend/_handler.js ↓</span></div>

```js
import express from 'express';
import { defaultHandler } from '@reshuffle/server-function';
import devDBAdmin from '@reshuffle/db-admin';

const app = express();

app.use("/dev/db-admin", express.json(), devDBAdmin.devDBAdminHandler);

app.use(defaultHandler);

export default app;
```

## Accessing the DB Admin Tool in your browser

To access your newly created admin page visit [localhost:3000/dev/db-admin](localhost:3000/dev/db-admin).

## Using the DB Admin Tool

Using the DB admin tool is straight forward. It provides access to all your key/value pairs stored in the database and from there you can:

1. Create a new key/value pair

2. Edit existing key/value pairs

3. Delete any or all key/value pairs within that database

### Learn more

If you want to take a deeper dive into the code and see the latest changes as they are submitted take a look at the source code [Reshuffle DB Admin Tool github](https://github.com/reshufflehq/reshuffle-db-admin).

## Conclusion

Reshuffle DB Admin Tool greatly improves upon your ability to edit a database on the fly. Weve done our best to provide a rich and powerful experience, without wasting your time worrying about messing up databases. As always, we live for feedback from our developers, so please let us know if you like or don't like what you see here.


<br />
<br />
<br />
