---
title: ReshuffleDB Queries
route: reshuffledb-queries
description: 'ReshuffleDB Queries'
category: 'Main Concepts'
priority: 12
---

# ReshuffleDB Queries 

The `set`, `get` and `update` methods of ReshuffleDB are perfect for managing simple state ([read more about those here](https://dev.reshuffle.app/building-the-hello-reshuffle-backend)), but when the data you’re working with is complex, you often need something more fine grained. To address these scenarios, ReshuffleDB surfaces a query mechanism which can be utilized to find and modify specific keys/values in your database.

## Writing a Simple Query

To demonstrate a simple query, we’ll need data to execute it on. For the sake of this example, let’s assume we’ve built a Reshuffle app that will track who will be invited to a birthday party. To facilitate this, we’ve stored each potential candidate in the DB, and prefixed their keys with either `friend_` or `foe_` to denote their current invite status. Here is a basic query on that DB, that will return all of the `friend_` keys:

<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/helloQuery.js ↓</span></div>

```js
import { Q, find } from '@reshuffle/db';

/* @expose */
export async function getAllFriendsNames() {
  const friendsQuery = Q.filter(Q.key.startsWith(‘friend_’));
  const allFriends = await find(friendsQuery);
  return allFriends.map(({ key }) => key);
}
```

To help us understand what’s happening here, we’ll go through this example item by item. 


The first line is generic and straightforward. Reshuffle queries primarily rely on two imports, `find` and `Q` (Query). We’ll go over these in more depth when we use them:

<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/helloQuery.js ↓</span></div>

```js
import { Q, find } from '@reshuffle/db';
```

The next item is our `getAllFriendsNames` function definition decorated with `@expose`. You don’t need to `@expose` a function to use a Reshuffle query, but we want `findAllFriends` to be accessible to our frontend:
 
<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/helloQuery.js ↓</span></div>

```js
/* @expose */
export async function getAllFriendsNames() {
```

Now we get to the interesting part. As we previously established, the function we’re writing needs to return all of the “friends” we’ve stored in the DB. To accomplish this, we’ll first define a query that filters all key that start with a specific prefix, `friend_`:

<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/helloQuery.js ↓</span></div>

```js
/* @expose */
export async function getAllFriendsNames() {
  const friendsQuery = Q.filter(Q.key.startsWith(‘friend_’));
```

The `Q` object API exposes a number of useful methods for constructing queries. The outer portion of the code, `Q.filter(...)` indicates that the desired result of the query is a filtered set of entries from the DB. The inner portion of the code, `Q.key.startsWith(‘friend_’)` describes what entries should be filtered. In this case we are filtering for keys that start with `friend_`.

> Note: Queries are not just limited to filtering. Other methods such as `all`, `any` and `not` are provided to ensure queries are as flexible as you need them to be. [Browse the API reference to see all the available methods](https://dev-docs.reshuffle.com/classes/_query_.query.html).

Now that we’ve constructed our query, it’s time to execute it. To execute a query, we will rely on the `find` method from ReshuffleDB.

<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/helloQuery.js ↓</span></div>

```js
/* @expose */
export async function getAllFriendsNames() {
  const friendsQuery = Q.filter(Q.key.startsWith(‘friend_’));
  const allFriends = await find(friendsQuery);
```

`find` returns a set of key/value pairs based on the specific query. This is great if we want both the key and value, but in this case we don’t. So the last line of the example uses ES6 `map` to return an array containing only the keys (and not the values).

<br />

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/helloQuery.js ↓</span></div>

```js
/* @expose */
export async function getAllFriendsNames() {
  const friendsQuery = Q.filter(Q.key.startsWith(‘friend_’));
  const allFriends = await find(friendsQuery);
  return allFriends.map(({ key }) => key);
}
```

This was just a basic example of what can be accomplished using Reshuffle queries. Far more is possible than what is covered here, [to learn more visit our reference docs](https://dev-docs.reshuffle.com/classes/_query_.query.html).

<br />
<br />
