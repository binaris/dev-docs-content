---
title: Building the Hello Reshuffle Backend
route: building-the-hello-reshuffle-backend
description: 'Building the hello Reshuffle backend'
category: 'Tutorial'
numbered: true
priority: 3
---

# Building the Backend from “Hello Reshuffle”

> This section continues work started in the previous section, [Writing Backend Logic](./writing-backend-logic)

While the hello world frontend we built has the notion of state, we did not persist that state anywhere (outside of the browser). This lack of persistence severely limits what can be done with the application, and how users interact with it. By utilizing the Reshuffle backend, in combination with the Reshuffle DB, this obstacle is easily overcome. 

The current frontend interface allows users to both retrieve and increment a numerical value. This means, that our backend will also need to support both of these paths. Start by creating a `helloServer.js` file in your backend directory. 

```sh
$ touch backend/helloServer.js # use "type NUL >> filename" on Windows
```

There are a few ways we could implement the logic needed to power our frontend. For this example, we’ll keep things simple and have a single function which is responsible for both getting and potentially adding to a numerical value. 

```js
/* @expose */
export async function addAndGet(num) {}
```

You may be wondering how this will work if the user only wants to retrieve a value and not add to the existing count. For this naive implementation, we will expect that users who want to strictly retrieve a value will simply pass in 0 for the amount they want to add. 

With the interface of our backend function defined, it’s time to make it “functional” 😂. To get things started, import `update` from `@reshuffle/db` at the top of your `helloServer.js` file.

```js
import { update } from '@reshuffle/db';
 
/* @expose */
export async function addAndGet(num) {}
```

The “update” operation in Reshuffle DB works almost identically to state update functions in React. Update takes a function that receives the `previousState` as an argument. The function supplied to `update` is required to return the `newState` which is the result of any updates you’ve applied. If that’s still a bit terse, here is the update code to finish off the helloServer.js backend.

```js
/* @expose */
export async function addAndGet(num) {
 return update('num', (prevNumber) => {
   if (prevNumber) {
     return num + prevNumber;
   }
   return num;
 });
}
```

Let’s go over what’s happening step by step

The first line signifies that we want to update the value stored at a key `num`. We also define an “updater” function that has a single arg `prevNumber` which represents the existing value possibly stored at `num`. The value is only possibly stored, because we have no guarantee that `update` has been called before!


```js
return update('num', (prevNumber) => {
```

To handle the case where update has not been previously called for `num`, we can explicitly check for the existence of `prevNumber` and only use it if it’s defined.

```js
if (prevNumber) {
  return num + prevNumber;
}
```

If `prevNumber` is undefined, we know that `update` has never been called for our key before. In that case, the new value is equal to whatever our user passed in.

```js
return num;
```

> Here’s the final state of `helloServer.js`
  <br />
  <div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/helloServer.js  ↓</span></div>

```js
import { update } from '@reshuffle/db';
 
/* @expose */
export async function addAndGet(num) {
 return update('num', (prevNumber) => {
   if (prevNumber) {
     return num + prevNumber;
   }
   return num;
 });
}
```

[Go to the next section to connect your frontend to your backend and finish the hello world example.](./calling-the-backend-from-the-frontend)

<br />
