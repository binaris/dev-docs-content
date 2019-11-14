---
title: Using ReshuffleDB
route: using-reshuffledb
description: 'Using ReshuffleDB'
category: 'Main Concepts'
priority: 12
---

# Using Reshuffle DB

ReshuffleDB is a key value store. It's capabilities include reading, writing and deleting single documents. ReshuffleDB surfaces four core operations `create`, `get`, `update`, and `remove` which allow you to conveniently modify and read data. `find` is also available if you need to query multiple documents, which you can read more about [here]([https://dev.reshuffle.app/reshuffledb-queries](https://dev.reshuffle.app/reshuffledb-queries)).

To use any of the capabilities provided by ReshuffleDB you must first import them from `@reshuffle/db` like so:

```js
import { create, get, update, remove } from '@reshuffle/db';
```

## Reference

- [create](#createkey-string-value-any-promise)
- [get](#getkey-string-promisejsonable--undefined)
- [update](#updatekey-string-updater-function-promise)
- [remove](#removekeyname-string-promise)
- [valid key types](#what-types-can-i-use-as-keys)
- [valid value types](#what-can-i-store-as-values)

---

### create(key: string, value: any): Promise<boolean>

```js
const created = await create('colors', ['red', 'blue', 'green', 'yellow']);
```

Create a document for the given key, returning `true` if the document was created and `false` if a key with given name already exists.

**Parameters:**

- **key:** `string`

    The key to create a document at.

- **value**: `JSONable`

    The initial document data you wish to store at **key**.

**Returns** `Promise<boolean>`

`true` if the document was created, `false` if the key already exists.

<hr style="height:1px; visibility:hidden;" />

---

### get(key: string): Promise<JSONable | undefined>

```js
const colors = await get('colors');
```

Retrieve a specified document with the given `key` from the DB. If the key does not exist, returns `undefined`.

**Parameters:**

- **key:** `string`

    The key of the document to retrieve.

**Returns** `Promise<JSONable | undefined>`

The object representation of the value stored at the key, or `undefined` if no value exists at the given key.

<hr style="height:1px; visibility:hidden;" />

---

### update(key: string, updater: function): Promise<JSONable>

```js
const updatedColors = await update('colors', (defaultColors = []) => {
	return colors.concat('purple');
});
```

Updates the document value at the specified key, creating a new document if the key did not previously exist. Updater function input argument will be `undefined` if the specified key does not already exist. The default initial value for the updater can be controlled using the [standard JavaScript default argument syntax]([https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)).

**Parameters**

- **key**: `string`

    The key of the document to update.

- **updater**: `function`

    Stateless function that gets the previous value and returns the next value to update the DB with, updater cannot return undefined. Update may be called multiple times when concurrent updates occur, so it should have no essential side effects.

**Returns** `Promise<JSONable>`

The updated document, as returned by the updater function.

<hr style="height:1px; visibility:hidden;" />

---

### remove(keyName: string): Promise<boolean>

```js
const removed = await remove('colors');
```

Remove a document at the given key, returning `true` if the document was removed and `false` if the specified key does not exist.

**Parameters**

- **key**: `string`

    The key of a document to delete.

**Returns** `Promise<boolean>`

`true` if document was deleted, `false` if the key does not exist.

<hr style="height:1px; visibility:hidden;" />

---

### **What types can I use as keys?**

Any valid unicode string is a valid DB key. We encourage using a path based schema for multiple namespaces, e.g:

    /users/<userID>

    /games/<gameID>

<hr style="height:1px; visibility:hidden;" />

---

### **What can I store as values?**

Values stored in the DB should be JSONable. You can store primitive types: strings, numbers, boolean values and null. We also support arrays and objects. Check out the [JSON spec](https://www.json.org/) if you have more detailed questions.

Values stored in the DB are read back to the user as stored. We do not guarantee any ordering on the keys.

- [Next, learn how to execute complex queries against ReshuffleDB] ([https://dev.reshuffle.app/reshuffledb-queries](https://dev.reshuffle.app/reshuffledb-queries))
