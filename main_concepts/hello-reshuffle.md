---
title: Hello Reshuffle
route: hello-reshuffle
description: 'The hello world program for Reshuffle'
category: 'Main Concepts'
priority: 0
numbered: true
---

# Hello Reshuffle

A minimal Reshuffle example:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> src/App.js  ↓</span></div>

```jsx
import '@reshuffle/code-transform/macro'
import React, { useState, useEffect } from 'react';
 
// import backend logic like any js function
import { addAndGet } from '../backend/helloServer.js';
 
export default () => {
 const [num, setNum] = useState(undefined);
 useEffect(() => {
   addAndGet(0).then(setNum)
 }, []);
 return (
   <div>
     <h1> Hello World from Reshuffle! </h1>
     <span> Number is: {num} </span>
     <button onClick={() => addAndGet(1).then(setNum)} >
       Increment me
     </button>
   </div>
 );
}
```

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> backend/helloServer.js  ↓</span></div>

```jsx
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

This example displays a numerical value stored in the Reshuffle DB. Pressing the button causes the value to increment and persist.

[Here is a link that will allow you to remix this app, and try it immediately](REPLACE_ME_WITH_REMIX_LINK)

Once you [remix](REPLACE_ME_WITH_REMIX_FAQ_LINK) the app, feel free to play with the values and specifics to see how everything fits together.

## Pre-existing Knowledge Assumptions

### Javascript

Reshuffle is a JavaScript library, so a basic understanding of JavaScript is expected. We always strive to keep things as simple as possible, but sometimes that means using newer features of JavaScript. Everything is constantly changing in the webdev world, and it can be very overwhelming to keep up to date. If you need to brush up, we highly recommend [this JavaScript tutorial (courtesy of Mozilla).](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript) 
Although at first, it might seem like stopping to learn fundamentals will slow you down, worry not. It will pay huge dividends in the long run.

> If you’re looking for something that explicitly addresses the recent additions to JavaScript, [this short overview (courtesy of Dan Abramov) is a great resource.](https://gist.github.com/gaearon/683e676101005de0add59e8bb345340c)

### React

The Reshuffle experience is built on top of [Create React App (CRA).](https://github.com/facebook/create-react-app) We do our best to assume minimum understanding of CRA or even React. That being said, a prior knowledge of React will reduce the amount of new information required considerably. 

The team at [reactjs.org](http://reactjs.org) does an amazing job with documentation (something that we’ve clearly drawn inspiration from). We’ve created a short list of some of the most crucial resources on [reactjs.org.](http://reactjs.org) These will be of great help if you’re feeling confused about a React concept you see used with Reshuffle.

* [Hello World](https://reactjs.org/docs/hello-world.html)
* [High Level API](https://reactjs.org/docs/react-api.html)
* [Hooks](https://reactjs.org/docs/hooks-intro.html)
* [Create React App Dev Docs](https://create-react-app.dev/docs/documentation-intro)

## Background

From the moment Reshuffle was incepted ([vintage Reshuffle](https://www.youtube.com/watch?v=rVXLZ4gYKGU)), the goal was clear. We wanted to provide a way for frontend developers to write fullstack applications, using the patterns and tools they were already comfortable with. We’ve done our best to make Reshuffle intuitive and predictable at every level. Unless specified otherwise, assume that things work the way you expect. We think you’ll be pleasantly surprised. If for any reason you’re not, we’re always available on [Discord](https://discord.gg/M8CC5hy) and we ❤️ feedback.

## What’s Next

* [Writing Frontend Logic](./writing-frontend-logic)
* [Writing Backend Logic](./writing-backend-logic)
* [Building the Hello Reshuffle Backend](./building-the-hello-reshuffle-backend)
* [Calling the Backend from the Frontend](./calling-the-backend-from-the-frontend)

<br />
<br />

This page is heavily inspired by: https://reactjs.org/docs/hello-world.html
