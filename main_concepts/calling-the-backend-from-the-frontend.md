---
title: Calling the Backend from the Frontend
route: calling-the-backend-from-the-frontend
description: 'Calling the Backend from the Frontend'
category: 'Main Concepts'
numbered: true
priority: 4
---

# Calling the Backend from the Frontend <br /> (A.K.A "Tying it All Together")

> This section continues work started in the previous section, [Building the Hello Reshuffle Backend](./building-the-hello-reshuffle-backend)

In this section, we will combine the frontend we built in [Writing Frontend Logic](./writing-frontend-logic) with the backend built in [Building the Hello Reshuffle Backend.](./building-the-hello-reshuffle-backend) By the end, we will have completely reconstructed the [Hello Reshuffle](./hello-reshuffle) app. In [Writing Frontend Logic](./writing-frontend-logic), we created a self-contained frontend that relies on local state to display a numerical value:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> src/App.js  ↓</span></div>

```jsx
import React, { useState } from 'react';
import './App.css';
 
function App() {
 const [num, setNum] = useState(undefined);
 return (
   <div>
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


and then a backend, which provides a way to query or increment a persistent numerical value:

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

In this section, we will finish creating the hello-world example, by connecting our frontend and backend together.

#### Using the Reshuffle backend from the frontend

Connecting the frontend to the backend is super simple with Reshuffle. Here are the two simple things you should know:

1. In every frontend file that intends to use the backend, import the reshuffle macro (only once per file) at the top of the file

    ```jsx
    import '@reshuffle/code-transform/macro';
    ```

    This macro provides the mechanism which makes the entire Reshuffle experience possible. At build time, our plugin analyzes any files that include this macro and intelligently replaces your local JavaScript backend calls with Reshuffle RPC calls.

2. Import the relevant `@expose` and `export` functions from your backend

	```jsx
    import { addAndGet } from '../backend/helloServer.js';
    ```

> Here is what that looks like in the context of our hello-world example.
<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> src/App.js  ↓</span></div>

```jsx
import '@reshuffle/code-transform/macro';
import React, { useState } from 'react';
 
// import backend logic as if it were available locally
import { addAndGet } from '../backend/helloServer.js';
 
export default () => {
 const [num, setNum] = useState(undefined);
```

After that, it’s just a matter of using `addAndGet` just as you would any other async JavaScript function. Let’s use this knowledge to swap our localized frontend state with the persistent version.

Start that process by modifying the `onClick` logic we wrote originally, to instead use our `addAndGet` backend function.

```jsx
<button onClick={() => addAndGet(1).then(setNum)} >
  Increment me
</button>
```

As you can see, we no longer directly use `setNum` to modify the local value. Instead, we call out to the `addAndGet` function, and then only update `setNum` after we’ve received the remote value from our backend.

This provides a semi-working version of the hello world app, but you’ll notice that refreshes to the page break the initial displayed value. To remedy this, let’s take utilize the [useEffect](https://reactjs.org/docs/hooks-effect.html) hook provided by React. `useEffect` allows us to write code that will only be called once per Component lifecycle, perfect for initialization. Start by adding the required `useEffect` import at the top of App.js

```jsx
import React, { useState, useEffect } from 'react';
```

Finally, let’s write a simple `useEffect` hook that re-uses the `addAndGet` function we previously set for the `onClick`.

```jsx
 useEffect(() => {
   addAndGet(0).then(setNum)
 }, []);
```

> We provide an empty array to `useEffect` to mimic the behavior of [ComponentDidMount](https://reactjs.org/docs/react-component.html#componentdidmount)

This hook specifies that we should call `addAndGet` with 0 as our input (which basically translates to “just get and don’t add”). The result of `addAndGet` is directly fed to `setNum` which should ensure the initial display reflects the persistent value. Refresh away!

Congratulations! You've just completed your first first app with reshuffle

<br />
<br />

<p style="margin: 0; padding: 0">
🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊
🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉
</p>
<div style="text-align: center; margin-top: 10px; margin-bottom: 15px; font-size: 32px"> Welcome to Reshuffle </div>
<p style="margin: 0; padding: 0">
🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊
🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉🎊🎉
</p>

<br />
<br />
<br />
