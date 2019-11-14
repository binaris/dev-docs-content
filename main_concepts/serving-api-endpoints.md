---
title: Serving API Endpoints
route: serving-api-endpoints
description: 'Serving API Endpoints with Reshuffle'
category: 'Main Concepts'
priority: 11
---

> Note: Your Reshuffle packages need to have the following minimum dependencies to utilize express functionality: 

```json
"@reshuffle/code-transform": "0.0.3",
"@reshuffle/db": "^0.5.3",
"@reshuffle/fetch-runtime": "0.0.6",
"@reshuffle/local-proxy": "^0.2.14",
"@reshuffle/server-function": "0.0.8",
```

# Serving API Endpoints

When developing fullstack applications, it’s often necessary to expose explicit endpoints that can either be consumed by your application or directly by users. While the traditional Reshuffle experience makes it incredibly convenient for your React frontend to communicate with the backend, it doesn’t provide a way to directly expose that backend to the outside world. To address this, the Reshuffle framework supports seamless integration with [express.js](https://expressjs.com/). 

## Adding Express to a Reshuffle app

The first step in adding an express server to a Reshuffle app, is to create a `_handler.js` file in your projects `backend` directory. 

```bash
$ touch backend/_handler.js # use "type NUL >> filename" on Windows
```

> It’s important to note that the file MUST be called `_handler.js`. This makes it possible for the Reshuffle runtime to confidently identify whether your app has an express server.

Now that we’ve created `_handler.js`, we need to install the express dependency into our project.

```bash
$ npm install --save express
```

### Writing a simple express server

Now that we have the boilerplate out of the way, let’s write a simple a simple “hello world” express server. The first step is to import express and the Reshuffle express handler into our `_handler.js` file:

<br />
<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/_handler.js ↓</span></div>

<br />

```js
import express from 'express';
import { defaultHandler } from '@reshuffle/server-function';
```

Next, we’ll create an express app so we can define routes for our server:

<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/_handler.js ↓</span></div>

```js
import express from 'express';
import { defaultHandler } from '@reshuffle/server-function';

const app = express();
```

Before we can define routes, we’ll need to utilize the `defaultHandler` middleware provided by Reshuffle:

<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/_handler.js ↓</span></div>

```js
import express from 'express';
import { defaultHandler } from '@reshuffle/server-function';

const app = express();

app.use(defaultHandler);
```

> Note: `defaultHandler` must always be the first middleware used by your express app

It’s important to understand what role `defaultHandler` serves. The `defaultHandler` is an [express middleware](https://expressjs.com/en/guide/using-middleware.html) which provides a mechanism to intercept HTTPS calls to your application, before Reshuffle does. This means that if you provide an express handler for the path [www.myreshuffleapp.com/hello](www.myreshuffleapp.com/hello), you should probably not have a React route (client side) for [/hello](/hello). There’s nothing explicitly stopping you from doing this, but you’re experience will be inconsistent at best.

We can almost start writing our express routes, but we need to make sure to export the express `app` as `default` at the bottom of our file:

<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/_handler.js ↓</span></div>

```js
import express from 'express';
import { defaultHandler } from '@reshuffle/server-function';

const app = express();

app.use(defaultHandler);

export default app;
```

 `default` is required because it provides the Reshuffle framework a deterministic way of importing your app. With all of the boilerplate out of the way, let’s write a simple route which responds with “Hello World”:

<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/_handler.js ↓</span></div>

```js
import express from 'express';
import { defaultHandler } from '@reshuffle/server-function';

const app = express();

app.get('/hello', function(req, res) {
   res.send(‘Hello world!’);
});

app.use(defaultHandler);

export default app;
```

That’s all it takes to add express to a Reshuffle app. Reshuffle express support and the decorator syntax aren’t mutually exclusive, so feel free to continue utilizing the decorator syntax for the rest of your app logic. 

### Reshuffle platform features and express

Express handlers can leverage all platform features such as ReshuffleDB. This means, you’re free to add logic that utilizes the data from your core application. Here is a minimal example:

<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/_handler.js ↓</span></div>

```js
import express from 'express';
import { defaultHandler } from '@reshuffle/server-function';

import { get } from '@reshuffle/db';

const app = express();

app.get('/hello', function(req, res) {
  // this assumes you’ve previously written data to the key “helloPhrase”
  const helloPhrase = (await get(‘helloPhrase’)) || ‘Hello World!’;
  return res.send(helloPhrase);  
});

app.use(defaultHandler);

export default app;
```

### Serving static content

You'll need to be aware of how path resolution differs between the cloud and local environment if you want to serve static content with express. `__dirname` will not work as this resolves differently based on which process originally ran the file. Here is an example of how to serve static assets from the `public` directory:

```js
app.use('/', express.static('./public'));
```
