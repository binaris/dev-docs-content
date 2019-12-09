---
title: Identity
route: identity
description: 'How to take advantage of Reshuffle identity'
category: 'Main Concepts'
priority: 10
---

> Note: Your Reshuffle packages need to have the following minimum dependencies to utilize Identity functionality: 

```json
"@reshuffle/code-transform": "^0.1.0",
"@reshuffle/db": "^0.5.4",
"@reshuffle/fetch-runtime": "^0.1.0",
"@reshuffle/local-proxy": "^0.3.1",
"@reshuffle/passport": "0.0.4",
"@reshuffle/react-auth": "^0.1.2",
"@reshuffle/server-function": "^0.2.1",
```


# Reshuffle Identity

At Reshuffle we're constantly reminded of how frustrating user authentication and identity management flows can be. Even integrating “out of the box” solutions will often have you wading through documentation and continuously scratching your head. Reshuffle identity focuses on simplifying this process, by providing an auth- zero-touch identity and authentication solution, that enables you to instantly add user support to your Reshuffle app.

## What is Reshuffle Identity?

Reshuffle identity has three major components:

1. Identity service which is automatically provisioned for each app. This service is operated and maintained on your behalf by Reshuffle.
1. Backend library which integrates with the service and handles session management for apps using Reshuffle identity.
1. Intuitive and modern client-side library which simplifies the process of adding identity to your Reshuffle app.

### Reshuffle Identity service

The Reshuffle Identity service is backed by Auth0 and requires no configuration. We handle the process of provisioning the tokens and credentials behind the scenes, so you don't have to. Reshuffle Identity is automatically added to new and existing Reshuffle apps, all you have to do is use it! 

### Reshuffle Identity backend library

The [Reshuffle Identity backend library](https://www.npmjs.com/package/@reshuffle/passport) integrates directly with Reshuffle client-side auth removing the need to directly create client/server sessions. This library also provides `/login` and `/logout` and `/whoami` endpoints for your app.

### Reshuffle Identity React library

The [Reshuffle React Auth library](https://www.npmjs.com/package/@reshuffle/react-auth) provides a set of client-side API’s which simplify and streamline the process of using Reshuffle Identity in your webapp. 

## Adding Reshuffle Identity to the backend

To support Reshuffle identity in your app you'll need to add the `authHandler` middleware to your apps express instance. This is mandatory, even if you plan to write the rest of your backend with decorated functions. Below is the minimal [Reshuffle API Serving](https://dev.reshuffle.app/serving-api-endpoints) file needed to support identity:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">backend/_handler.js ↓</span></div>

```js
import express from 'express';
import { defaultHandler } from '@reshuffle/server-function';
import { authHandler } from '@reshuffle/passport';

const app = express();
app.use(authHandler);

app.use(defaultHandler);

export default app;
```

The `authHandler` middleware is responsible for three things:

1. Adds a `/login` endpoint to login users
1. Adds a `/logout` endpoint to logout users
1. Automatically creates and maintains sessions for logged in users (demonstrated below)

Aside from the required boilerplate, `authHandler` adds automatic session support for your app. The `user` object will contain profile information pertaining to the user who originated the request. The user is available to express endpoints via `req.user`:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">backend/_handler.js ↓</span></div>

```js
const app = express();
app.use(authHandler);

app.get(‘/get-user-todos', (req, res) => {
  const { id } = req.user;
  // get all todolist
  return get(`/todos/${id}`);
});

app.use(defaultHandler);

export default app;
```

If you're using decorated functions, you'll access the session via `getCurrentUser`. Here's an example that uses `getCurrentUser` to fetch a users todos:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">backend/hello.js ↓</span></div>

```js
import { get } from ‘@reshuffle/db';
import { getCurrentUser } from '@reshuffle/server-function';

/* @expose */
export async function getTodoList() {
  const { id } = getCurrentUser(true);
  // get all todolist
  return get(`/todos/${id}`);
}
```

`getCurrentUser` takes a single optional boolean argument which indicates if the request should fail if there is not a current user stored in the session.

## Adding Reshuffle Identity to the frontend

Reshuffle provides a React based (other frameworks coming soon) library that seamlessly integrates with Reshuffle identity. Before you can start using it, you'll need to install two dependencies [@reshuffle/react-auth](https://www.npmjs.com/package/@reshuffle/react-auth) and [@reshuffle/passport](https://www.npmjs.com/package/@reshuffle/passport) via npm:

```bash
npm install @reshuffle/react-auth @reshuffle/passport
```

Now that things are properly installed, we'll need to wrap our top level `App` component in a Reshuffle `AuthProvider`:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)"> src/index.js ↓</span></div>

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

import { AuthProvider } from '@reshuffle/react-auth';

import App from './App';

ReactDOM.render((
  <AuthProvider>
    <App />
  </AuthProvider>
), document.getElementById('root'));
```

The `AuthProvider` utilizes [React Context](https://reactjs.org/docs/context.html) to propagate auth state throughout the rest of your app. For this reason, you'll most likely want to wrap your highest level component with the `AuthProvider`.

Now that we've configured the provider, we can start adding basic login/logout functionality to our site. The first step is to import a hook provided by Reshuffle, that handles the tricky parts of authentication and identity management for you.

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">src/App.js ↓</span></div>

```jsx
import { useAuth } from '@reshuffle/react-auth';
```

`useAuth` provides a set of variables that track the state of auth for the current logged in user. Also provides application specific URL's that allow users to login to your site.

At the top of our `App.js` we'll utilize `useAuth` to build our simple auth example:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">src/App.js ↓</span></div>

```jsx
export default function App() {
  const {
    loading,
    error,
    authenticated,
    profile,
    getLoginURL,
    getLogoutURL,
  } = useAuth();
  ...
```

Now that we have our hook setup, we'll create a simple view that represents the current auth state of your Reshuffle app. First we'll handle loading transitions, `useAuth` provides the `loading` variable that indicates whether the app is in a loading state.  We'll utilize that to conditionally render a loading view for our app:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">src/App.js ↓</span></div>

```jsx
const {
  loading,
  error,
  authenticated,
  profile,
  getLoginURL,
  getLogoutURL,
} = useAuth();

if (loading) {
  return <div><h2>Loading...</h2></div>;
}
```

`useAuth` also provides the `error` variable that represents a potential error message associated with auth. Once again, let's use that to conditionally render an error view:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">src/App.js ↓</span></div>

```jsx
if (loading) {
  return <div><h2>Loading...</h2></div>;
}

if (error) {
  return <div><h1>{error.toString()}</h1></div>;
}
```

Now that we've handled those cases, let's create a simple view that enables users of our app to login and logout. We will accomplish this using the `getLoginURL` and `getLogoutURL` functions provided by `useAuth`.

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">src/App.js ↓</span></div>

```jsx
return (
  <header>
    <div>
      <h2>Reshuffle Auth</h2>
    </div>
    <div>
    {
      authenticated ? (
        <>
          <img src={profile.picture} height={20} />
          <span>{profile.displayName}</span>
          <a href={getLogoutURL()}>Logout</a> </>
      ) : (
        <a href={getLoginURL()}>Login</a>
      )
    }
    </div>
  </header>
);
```

Let's quickly cover what's happening here. Within our inner div, we're conditionally rendering the users profile information based on the current value of `authenticated` provided by `useAuth`. In the case that the user is authenticated, we display some basic profile information such as their picture and display name along with a logout link. In the case that the user is not authenticated, we render a single link, which will allow users to login to your app when clicked. Here is the final version of `App.js`:



<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">src/App.js ↓</span></div>


```jsx
import '@reshuffle/code-transform/macro';
import React from 'react';

import { useAuth } from '@reshuffle/react-auth';

export default function App() {
  const {
    loading,
    error,
    authenticated,
    profile,
    getLoginURL,
    getLogoutURL,
  } = useAuth();

  if (loading) {
    return <div><h2>Loading...</h2></div>;
  }

  if (error) {
    return <div><h1>{error.toString()}</h1></div>;
  }

  return (
    <header>
      <div>
        <h2>Reshuffle Auth</h2>
      </div>
      <div>
      {
        authenticated ? (
          <>
            <img src={profile.picture} height={20} />
            <span>{profile.displayName}</span>
            <a href={getLogoutURL()}>Logout</a>
          </>
        ) : (
          <a href={getLoginURL()}>Login</a>
        )
      }
      </div>
    </header>
  );
}
```

### Using auth with class components

In addition to the `useAuth` hook, we provide direct access to the AuthContext allowing auth to be utilized in class components. A simple example demonstrating Context usage in a class component is shown below:

<div style="text-align: right;"><span style="padding: 1%; background-color: rgba(35, 191, 98, 0.5)">src/App.js ↓</span></div>


```jsx
import '@reshuffle/code-transform/macro';
import React from 'react';
import { AuthContext } from '@reshuffle/react-auth';

export default class App extends React.Component {
  static contextType = AuthContext;
  
  render() {
    const {
      loading,
      error,
      authenticated,
      profile,
      getLoginURL,
      getLogoutURL,
    } = this.context;

    if (loading) {
      return <div><h2>Loading...</h2></div>;
    }

    if (error) {
      return <div><h1>{error.toString()}</h1></div>;
    }

    return (
      <header>
        <div>
          <h2>Reshuffle Auth</h2>
        </div>
        <div>
        {
          authenticated ? (
            <>
              <img src={profile.picture} height={20} />
              <span>{profile.displayName}</span>
              <a href={getLogoutURL()}>Logout</a>
            </>
          ) : (
            <a href={getLoginURL()}>Login</a>
          )
        }
        </div>
      </header>
    );
  }
}
```

<br />

### Profile API

Below is the API of the `profile` object returned by Reshuffle Identity:

```ts
interface Profile {
  provider: string;
  id: string;
  displayName: string;
  emails?: Email[];
  picture?: string;
}
```

### Opening Reshuffle Identity in a new window

It's possible to open the login view in a new window. To do so, follow the pattern demonstrated below:

```jsx
  ...

    getLoginURL,
    getLogoutURL,
    login,
  } = useAuth();
  
  ...
  
  return (
    <a href='/login' onClick={(e) => {
      login({ newWindow: true }); 
      e.preventDefault();
    }}>
      Login from new window
    </a>
  );
}
```

### Setting a custom login redirect link

It's possible to set a custom `returnTo` URL for the login link. To accomplish this, `getLoginURL` takes in an optional `returnTo` argument. The path provided must be a fully qualified path (ie: `mysite.com/somepath/path`) and not just a relative link (ie: `/path`). Here is a generic way to handle this between local/remote development


```jsx
getLoginURL(`${window.location.origin.toString()}/hello`)
```

## Conclusion

Reshuffle Identity greatly reduces the barrier of entry required to support users for new and existing apps. We've done our best to provide a rich and powerful experience, without wasting your time worrying about configuration and security. As always, we live for feedback from our developers, so please let us know if you like or don't like what you see here.



<br />
<br />
<br />
