---
title: Secret Variables
route: secret-variables
description: 'Using secret variables'
category: 'Main Concepts'
priority: 14
---

# Secret Variables

When developing apps, there is often a need to rely on sensitive credentials and variables. From a security standpoint, it's almost never a good idea to write these sensitive values directly into your code. This is especially true if your app is managed with source control. To address this, Reshuffle provides a convenient and secure mechanism to inject variables into your apps at runtime.

## Creating a Secrets File

Reshuffle uses the common [dotenv](https://www.npmjs.com/package/dotenv) format to control the secret variables for an app. For those unfamiliar, dotenv looks for a well named file `.env` which may contain any number of key/value pairs, each on their own line. Here's a practical example of a `.env` file:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> my-reshuffle-app/.env ↓</span></div>

```yaml
SECRET0=13231231313
secretUrl = https://my-secret-url.com
auth_secret=CRYPTOGRAPHIC-MAGIC
```

The `.env` file format adheres to the same rules as a YAML file. This means that there is no need to quote/escape strings or numbers. We highly recommend adding the `.env` file to your `.gitignore`, that way you'll never accidentally upload sensitive credentials to your repository.

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> example .gitignore  ↓</span></div>

```bash
# See https://help.github.com/articles/ignoring-files/ for more about ignoring files.

# dependencies
/node_modules
/.pnp
.pnp.js

#misc
.env
```

_All 1st party Reshuffle templates come with .env already in the .gitignore_

## Utilizing Secrets

Once you've added secrets to the `.env` file in your projects root directory, you can access them anywhere in your backend. Secrets are surfaced as environment variables at runtime, meaning that you can access them using the standard NodeJS [`process.env`](https://nodejs.org/api/process.html#process_process_env). The below code demonstrates accessing the variables we defined in the previous sections fake `.env` file.


<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/helloServer.js ↓</span></div>

```js
import { update } from '@reshuffle/db';
import { loadAuth } from './some-auth-file.js';

const { SECRET0, secretUrl, auth_secret } = process.env;

// initialize some auth using our secret
const auth = loadAuth(auth_secret);
```

> Secrets work consistently across remote and local development, so don't stress about writing two different versions of the code based on the runtime environment. [Here is a template that utilizes secrets](https://github.com/reshufflehq/dev-docs).
