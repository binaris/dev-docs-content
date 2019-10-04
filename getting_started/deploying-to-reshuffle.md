---
title: Deploying to Reshuffle
route: deploying-to-reshuffle
description: "Deploying to Reshuffle"
category: "Getting Started"
priority: 2
---

# Deploying to Reshuffle
This section covers deploying your local code back to Reshuffle. We assume you have read and executed the steps in the [previous section](https://dev.reshuffle.app/running-locally). 

**1. Run the deploy script**

Once you have a locally working app you are happy with, you will want to deploy it back to Reshuffle. In your command line, go  the project’s root folder and run:

```js
npx reshuffle deploy
```

If you have not authenticated before, this script will walk you through a web authentication process using your GitHub account. This authentication process ensures only you can deploy and manage your apps. 

<br>
<img src="https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/deploy-to-reshuffle1.png?token=AAR6X6ZKWVEFWMJ2XMAXR3K5S3EOU" alt="drawing" style="width:400px;"/>

Once you connect your GitHub account, return to the command line. At this point, Reshuffle CLI might prompt you to select the project you want to deploy to. This only happens when Reshuffle is unsure  which app you are targeting for deployment. After this is done, Reshuffle will deploy your app (including both backend and frontend) to your online app.  

You're done! Enjoy your new app!

**2. Bonus points: Join the community**

Be a part of our community on Discord - [join here](https://discordapp.com/channels/612049440047497217/612049440047497219).  If you are feeling extra awesome, you should create and share your own template with the community. This way other developers will be able to innovate on top of it. Here is how to [submit your  own template](https://dev.reshuffle.app/submitting-a-template).
