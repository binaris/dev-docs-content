---
title: Writing Frontend Logic
route: writing-frontend-logic
description: 'Writing frontend logic for Reshuffle'
category: 'Main Concepts'
priority: 1
numbered: true
---

# Writing Frontend Logic

> Over the next 4 sections, we will go through the steps required to build the “hello Reshuffle” app <br /> ([as seen in the previous section](./hello-reshuffle)).

In this section, we will build the frontend portion of the “hello Reshuffle” app. To follow along, [click here to “remix”](https://reshuffle.com/template/counter-hooks) the boilerplate Reshuffle template. When you remix an app with Reshuffle, the app (code and resources) are copied to your account and immediately made available. 

Here is the App.js file of the Reshuffle boilerplate template (it is exactly like what you would get from [Create React App](https://github.com/facebook/create-react-app)):


<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> src/App.js  ↓</span></div>

```jsx
import React from 'react';
import logo from './logo.svg';
import './App.css';
 
function App() {
 return (
   <div className="App">
     <header className="App-header">
       <img src={logo} className="App-logo" alt="logo" />
       <p>
         Edit <code>src/App.js</code> and save to reload.
       </p>
       <a
         className="App-link"
         href="https://reactjs.org"
         target="_blank"
         rel="noopener noreferrer"
       >
         Learn React
       </a>
     </header>
   </div>
 );
}
 
export default App;
```

> When writing the frontend of a Reshuffle app, it’s often easiest to understand Reshuffle as a superset of [Create React App (CRA)](https://github.com/facebook/create-react-app). In other words, if it works in CRA, it should work in Reshuffle (but not necessarily vice versa).

## Building the “Hello Reshuffle” Example

Before we get started, let’s do some cleanup. Remove most of the boilerplate content in App.js, so you’re left with the following:


<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> src/App.js  ↓</span></div>

```jsx
import React from 'react';
import './App.css';
 
function App() {
 return (
   <div>
     <h1> Your place to shine! </h1>
   </div>
 );
}
 
export default App;
```

_If you remixed, you should see “Your place to shine!” in your browser._

<br />

Now that we have a “blank canvas”, let’s start by defining the general layout of our page. The [hello reshuffle example](./hello-reshuffle) has two primary elements.

<br />

1. A text element that displays a dynamic number (using a `<span />`) 

	```jsx
    <span>
      Number is:
    </span>
    ```

2. An interactive element which allows you to increase that number by one (using a `<button />`)

    ```jsx
    <button>
      Increment me
    </button>
    ```



> Here’s what App.js looks like at this point:
<div style="text-align: right;"><span style="text-align: right; padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> src/App.js  ↓</span></div>

```jsx
function App() {
 return (
   <div>
     <h1> Your place to shine! </h1>
     <span>
       Number is:
     </span>
     <button>
       Increment me
     </button>
   </div>
 );
}
```

Now that we have our basic layout, continue by creating a stateful value to plug into the <span>. We can accomplish this through React’s [“useState”](https://reactjs.org/docs/hooks-state.html) hook. 

1. Import `useState` from React

    ```jsx
    import React, { useState } from 'react';
    ```

2. Initialize the state hook at the start of our function component. We don’t want to start with a number in our state, so pass in `undefined` as the initial argument

    ```jsx
    function App() {
      const [num, setNum] = useState(undefined);
      return (
      ...
    ```

3. Finally, plug the `num` value (returned from useState) into the `<span>`

    ```jsx
    <span>
      Number is: {num}
    </span>
    ```

With the display portion of our Component finished, we’ll want a way to increase the number. In the next section, we’ll go through the steps of connecting the button to your Reshuffle backend, for now, let’s just get it working within the App component.

```jsx
<button onClick={() => setNum((prevNum) => 1 + (prevNum || 0))}>
  Increment me
</button>
```

This should result in a working, frontend-only version of the hello Reshuffle example. There are some small issues (eg: the initial number displayed is undefined instead of 0), these will get fleshed out in a [future section](./calling-the-frontend-from-the-backend).

> Let’s look at the full example:
<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> src/App.js  ↓</span></div>

```jsx
import React, { useState } from 'react';
import './App.css';
 
function App() {
 const [num, setNum] = useState(undefined);
 return (
   <div>
     <h1> Your place to shine! </h1>
     <span>
       Number is: {num}
     </span>
     <button onClick={() => setNum((prevNum) => 1 + (prevNum || 0))}>
       Increment me
     </button>
   </div>
 );
}
 
export default App;
```

Here is the app live on Reshuffle:
<iframe src="https://meaningful-nightingale-45.reshuffle.app" width="400" height="300"> </iframe>
<br /><br />

In the [next tutorial](./writing-backend-logic), we’ll add a backend and save our number state persistently!

<br />
<br />
<br />