---
title: About Reshuffle  
route: about 
description: 'Terms of Service'
category: 'Other Goodies'
priority: 3
---

# About Reshuffle 
**Our mission is to make developers more creative.** We do that by making you more productive and helping you share your best work with other developers.

Reshuffle enables [React](https://reactjs.org) developers to build end-to-end applications without managing the cloud. Simply add backend code to your React project, and we will deploy your code to the cloud and scale to handle thousands of users and millions of requests.

Reshuffle is a community of developers sharing and reusing code to build better applications. You can start new projects from any of the many templates on our site. You are welcome to share your code back as templates for other people to start from.

## Right now, everything is free
Our free cloud tier is available today. You can deploy and run any app with the following limits:

- 1000 requests per second

- 1 second request timeout

- 1GB data and files storage

In the future, we will offer an unlimited premium tier. We will soon release an open source runtime, so you can run apps in your own environment.

## How it works

Reshuffle apps are built around [Create-react-app](https://github.com/facebook/create-react-app). After remixing an app and downloading its code, simply run *npm install && npm start*. You can then edit your app using your favorite tools the familiar interactive Webpack workflow we all ❤️

```js
npm install && npm start
```

Add backend code directly into your React project. All Reshuffle apps include a backend folder where you place your backend files. Backend code can be written with plain JavaScript, meaning you can use advanced ES7 features and any npm package you require (ha!).

Annotate your endpoint functions so that Reshuffle knows which functions to make available to the frontend and which can only be called by other backend functions.

We comment out the @expose decorator until decorators become an official part of JavaScript 🤞

```js
/**
 * Form customized greeting.
 *
 * @return { Promise<string> } - greeting text
 */
/* @expose */
export async function greet(name) {
  return `Hello ${name}!`;
}
```

No HTTP required to call a backend function. We automatically replace native JavaScript function calls with HTTP requests to the backend. We handle argument encoding, error codes and network error for you. All you have to do is call a function.

```js
import React, { useState, useEffect } from 'react';
import ReactDOM from 'react-dom';
import { greet } from '../backend/greeting';
​
function App() {
  const [greeting, setGreeting] = useState(undefined);
​
  useEffect(() => {
    if (greeting === undefined) {
      greet('world').         // <- Magic happens here
        then(setGreeting);
    }
  }, []);
​
  return greeting ? (<h1>{greeting}</h1>) : 'Loading...';
}
​
ReactDOM.render(
  <App/>,
  document.getElementById('root')
);
```

Develop locally. Your backend code is automatically synchronized to a local dev server. The same interactive experience Webpack provides for your React code, is now available for backend code as well.

<img src="https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/hello_world.png?token=AAR6X63TBY7BH3INTOBIJXK5SZ6Q4" alt="drawing" style="width:600px;"/>

Deploy to the cloud. When you are ready to share your work with others, simply run npx reshuffle deploy to deploy your code onto our scalable cloud infrastructure.

```js
npx reshuffle deploy
```

## A simple idea

Today, most apps consist of three parts: frontend code, backend code and data. Often these independent pieces are built and maintained by different people.
The idea behind Reshuffle is very simple. We integrate frontend, backend and data into a single fully-functional unit. This allows us to run any such unit with a click of a button, because it already contains everything it needs in order to run. It also allows us to scale resources as needed to accomodate load.
This unified structure allows you to build fully functional applications, without handling the complexities of distributed backend coding and cloud operations.

[TODO: image]


## We are developers

<table>
 <tr>
   <td><b>Michael Adda</b><br/>
     <img alt="Michael" src="https://binaris.com/jobs/images/michael_adda.png"/><br/>
     Co-founder & CTO, father, kernel surgeon, <a href="https://nethack.org/common/index.html">nethack</a> addict, wears pink
   </td>
   <td><b><a href="https://github.com/bergundy">Roey Berman</a></b><br/>
     <img alt="Roey" src="https://avatars1.githubusercontent.com/u/52304?s=256&v=4" /><br/>
     There's only one book in my library, and that's
     <a href="https://en.wikipedia.org/wiki/The_C_Programming_Language">The Bible</a>
   </td>
 </tr>
 <tr>
   <td><b>Avner Braverman</b><br/>
     <img alt="Avner" src="https://binaris.com/jobs/images/avner_braverman.png"/><br/>
     Co-founder & CEO, HPC by trade, UX by passion
   </td>
   <td><b>Ryland Goldstein</b><br/>
     <img alt="Ryland" src="https://binaris.com/jobs/images/ryland_goldstein.png" /><br/>
     Binaris California head, United frequent flyer
   </td>
 </tr>
 <tr>
   <td><b>Arik Maor</b><br/>
     <img alt="Arik" src="https://binaris.com/jobs/images/arik.jpg" height="250" /><br/>
     Cat lover, custom standing desk owner
   </td>
   <td><b>Nimo Naamani</b><br/>
     <img alt="Nimo" src="https://avatars0.githubusercontent.com/u/2087890?s=256" height="250"/><br/>
     The NZ delegate, Hiker. Forever learning.
   </td>
 </tr>
 <tr>
   <td><b>Ariel Shaqed (Scolnicov)</b><br/>
     <img alt="Ariel" src="https://binaris.com/jobs/images/ariel_shaqed__scolnicov_.png"/><br/>
     Stops coding early twice a week to enjoy 3 kids.  I have a slide rule
     and I'm not afraid to use it!
   </td>
   <td><b>Amir Shevat</b><br/>
     <img alt="Amir" src="https://binaris.com/jobs/images/amir-shevat.jpg" height="250" /><br/>
     Co-founder & CPO, husband of one, father of two + a cat and a dog. Author of <a href="https://www.amazon.com/Amir-Shevat/e/B072C99151">books</a>.
   </td>
 </tr>
 <tr>
   <td><b>Olga Zelenko</b><br/>
     <img alt="Olga" src="https://binaris.com/jobs/images/olga_zelenko.jpg" height="250" /><br/>
     Mother, wife, photographer and designer at heart
   </td>
   <td><b>Vladimir Zoubritsky</b><br/>
     <img alt="Vladimir" src="https://binaris.com/jobs/images/vladimir_zoubritsky.png" /><br/>
     Embarrassingly parallel programmer, mechanical keyboards collector
   </td>
 </tr>
</table>

