---
title: Running Locally
route: running-locally
description: "Running Reshuffle locally"
category: "Getting Started"
priority: 1
---

# Working locally
This section covers how to download an app template and modify it to make it to meet your needs. We assume you have read and executed the steps in the [previous section](https://dev.reshuffle.app/starting-from-a-template). 

**1. Download your template**

On the post Remix page, you will find information on how to download your template project.
<br><br>
<img src="https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/running-locally1.png?token=AAR6X64MF2GUM4QW3YSAA7C5S3DDY" alt="drawing" style="width:600px;"/>


You can  install the code directly using the npx command  provided. Alternatively, you can just download the zip file of the template code. The command downloads the code, and immediately runs npm install. if you choose to download the zip file, you will need to run npm install yourself inside the unzipped folder. 

**2. Edit your code**

Now that you have the app on your machine, you can edit and run it in the same awesome way you would with any other [create-react-app](https://create-react-app.dev/) web application. In addition to the src/ folder that react provides for your frontend code, you will notice that reshuffle adds a backend/ folder to edit and manage your backend code. You will also be provided with a local database, so you can test and build your full-stack app locally. Read more on the Reshuffle programming model [here](https://dev.reshuffle.app/hello-reshuffle). 

Once you run `npm start`, Reshuffle will run a local process that will mimic the backend code and database functionality. You will be able to save data locally and use the [Reshuffle API](https://dev-docs.reshuffle.com/) in the same manner you would in the cloud.  If you run into issues please reach out to us on the [Discord](https://discordapp.com/invite/M8CC5hy) channel. 

Once you are happy with your app, you can deploy it back to your Reshuffle live app. We will talk about that in the [next section](https://dev.reshuffle.app/deploying-to-reshuffle). 

