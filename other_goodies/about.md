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

[todo: image]

Deploy to the cloud. When you are ready to share your work with others, simply run npx reshuffle deploy to deploy your code onto our scalable cloud infrastructure.

[TODO: cmd]

## A simple idea

Today, most apps consist of three parts: frontend code, backend code and data. Often these independent pieces are built and maintained by different people.
The idea behind Reshuffle is very simple. We integrate frontend, backend and data into a single fully-functional unit. This allows us to run any such unit with a click of a button, because it already contains everything it needs in order to run. It also allows us to scale resources as needed to accomodate load.
This unified structure allows you to build fully functional applications, without handling the complexities of distributed backend coding and cloud operations.

[TODO: image]


## We are developers

[TODO: markdown]

