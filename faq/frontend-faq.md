---
title: Frontend FAQ
route: frontend-faq
description: 'Frontend framework frequently asked questions'
category: 'FAQ'
priority: 0
---

# Reshuffle Frontend Framework

### Question: Can I use Reshuffle with my existing Create React App project?

Answer: It's always possible to move your existing projects assets/files to the "Blank" Reshuffle template manually. An official conversion process is a priority for us, keep an eye on our [roadmap](https://trello.com/b/e4Hfp3cB/public-roadmap).

### Question: What are the differences between Reshuffle and CRA?

Answer: We extend CRA to support backend code and a database. We maintain the same interactive developer experience we all know and love, and add support for backend code and data access. Our APIs are compatible between your local development environment and the cloud.

### Question: Can I use Reshuffle with other Single Page Application frameworks such as Vue and Angular?

Answer: Reshuffle currently supports Create React App out of the box. If support for Vue and Angular is important to you, we would love to hear about it!

### Question: Does Reshuffle support React Native?

Answer: We love React Native here at Reshuffle. Although we currently don't support React Native, it's something we're very interested in, so keep an eye on our [roadmap](https://trello.com/b/e4Hfp3cB/public-roadmap).

### Question: Is it possible to integrate state management solutions (such as Redux/Mobx) with Reshuffle?

Answer: We don’t provide specifics tools for integrating Redux or Mobx, but we don’t do anything to prevent it. As always, PR’s and community additions are always appreciated!

### Question: Is there support for editor integration such as a VSCode plugin?

Answer: Reshuffle works with any editor of your choosing. We do not currently have a plugin in any of the major editors. If this is something important to you, we would love to hear about it!

### Question: How can I use environment variables in my frontend with Reshuffle?

Answer: We support environment variables via Create React App, [read the docs to learn more](https://create-react-app.dev/docs/adding-custom-environment-variables)!


### Question: Can I access my Reshuffle DB directly from my frontend?

Answer: Your frontend code can call backend functions that access the database directly. In the future we will add push notification and subscription mechanisms to update the frontend directly when database changes occur. Keep an eye on our [roadmap](https://trello.com/b/e4Hfp3cB/public-roadmap).

### Question: Does Reshuffle have a frontend auth library?

Answer: Reshuffle works with any existing OAUTH2 framework, keep using the libraries you know and love. [We even have a template that utilizes Google auth](https://github.com/reshufflehq/dev-docs). Our [roadmap](https://trello.com/b/e4Hfp3cB/public-roadmap) has this use case in mind, and as always PR’s and community additions are always appreciated!

### Question: Is it possible to only redeploy my frontend?

Answer: Reshuffle currently deploys your entire application (frontend and backend).

### Question: How much will my bundle size increase when using Reshuffle?

Answer: Reshuffle only adds a single file (with a trivial size) to your bundle.

### Question: Does Reshuffle frontend support TypeScript?

Answer: It does!

### Question: Can I use Reshuffle in conjunction with services such as Pusher?

Answer: Absolutely!

### Question: Do I have to await calls to the backend?

Answer: All calls to the backend must be invoked with `await` or using the `.then()...catch()` pattern. This usage is required to properly handle potential backend errors.

### Question: Can I make multiple (parallel) calls to the backend?

Answer: Definitely, you should never have to worry about the distributed nature of your application when using Reshuffle.

### Question: How can I handle errors from the Reshuffle backend?

Answer: Calls to the backend return Promises(link) which are resolved only if the backend function successfully returned a value. In case of an error, the Promise is rejected (or throws an exception if you use await).

### Question: Are there automatic retries on backend calls? Is there a library or mechanism that can make this possible?

Answer: We do our best to ensure all your backend calls run successfully. We currently do not automatically retry requests, so we recommend wrapping your backend calls in a try-catch clause and manually retrying if necessary.

### Question: Do all browsers support Reshuffle?

Answer: Most modern browsers support Reshuffle, including Chrome, Firefox and Safari.

### Question: Do I have to import the Reshuffle macro in every file?

Answer: Only files that make calls to a Reshuffle backend.

### Question: What will happen if I forget to import the Reshuffle macro?

Answer: An informative error will be returned pointing you to the missing macro.

### Question: How can I add Google Analytics to my Reshuffle project?

Answer: We recommend using the canonical [react-ga](https://github.com/react-ga/react-ga) package available via npm.