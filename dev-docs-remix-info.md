---
title: Example Content
route: example-content
category: 'Main Concepts'
---

# Developer Documentation Template

This template serves as a generic "developer documentation" site. It boasts features such as:

* Content as markdown
* Markdown supports nested HTML (for when markdown isn't enough)
* Support for syntax highlighting (including JSX)
* Real-time editor and admin page which serves as a basic CMS
* Responsive (works great on mobile or desktop)
* Near perfect Google lighthouse score

## Getting Started

Before deploying the template, you'll need to configure your environment, along with some external resources. To accomplish this, we recommend adding a `.env` file in the directory that contains this project. The `.env` file should have the following variables defined.

**JWT_HMAC_KEY**

Private key used to sign authentication tokens on the backend. This key should be long and secure (either using a private key or a [site like this](https://www.uuidgenerator.net/)). 

> Note: the `JWT_HMAC_KEY` controls all access to your site administration, keep it safe!


**REACT_APP_VALID_HOSTED_DOMAIN**

With the current design, this template only works if you have a Google organization with its own [hosted domain.](https://developers.google.com/identity/protocols/OpenIDConnect#hd-param) This mechanism limits admin access to Google users with a `@<YOUR_HOSTED_DOMAIN>` email address.

> Note: if this is set to `gmail.com` any gmail user will have admin access to your site!


**REACT_APP_OAUTH_CLIENT_ID**

To utilize the Google-based login featured in this template, you'll need to create your own Google project. If you haven't done this already, [follow the steps described in this Google documentation.](https://developers.google.com/identity/protocols/OAuth2). Make sure to add your Reshuffle app URL as a valid origin domain on the "Credentials" page for your Google project ([Here is the generic version of that URL](https://console.developers.google.com/apis/credentials/oauthclient/)). 



**REACT_APP_AUTH_NAME**

Name that will be displayed on the admin login button. For example, if you set `REACT_APP_AUTH_NAME` to "My Project", the text would display as

![](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/auth-button-example.png)


### Adding Content

To add content on the site, navigate to `https://<base-url>/editor`. At this point, you'll be asked to authenticate using your previously configured Google OAuth credentials. After successfully authenticating, you'll be redirected to the editor page.

![](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/dev-editor-screen.png)

_The editor page_

The bottom half of the page can be used to write markdown, which will be parsed and displayed in real time. The "Update" button will update the content that you're currently editing (or create it if it doesn't exist). "Select a Post" allows you to retrieve existing posts and edit them as desired.

For a post to be recognized and displayed by the site, it must include a frontmatter with the following keys (additional keys are ok, these ones are required):

```yaml
---
title:
route:
category:
---
```

**Title** controls the displayed name of the content on your site. 

**Route** determines what sub-URL the content will be available at. Valid routes can only contain lowercase letters, numbers and dashes (no spaces). For example, if my route was 'example-content', the content would be available at `https://<base-url>/example-content`.

**Category** controls the sidebar category that your content will be displayed in. Note that this isn't strictly required, although your content will be completely hidden if omitted. Currently, the valid categories are:

* Getting Started
* Main Concepts
* Other Goodies


> When posts are created, they are initially disabled by default. You'll need to visit the `/admin` page to enable your post.

### Managing Content

To manage content on the site, navigate to `https://<base-url>/admin`. Similarly to the `/editor` page, you'll be asked to authenticate using your previously configured Google OAuth credentials. After successfully authenticating, you'll be redirected to the `/admin` page.

![](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/dev-admin-screen.png)

_The admin page_

The admin page provides mechanisms to enable, disable and delete pages. A home page for the site can also be set, using the "Set as home" button.

> Note: only a single page can be set as the home route


We love feedback! To provide feedback about this template (or any other part of the Reshuffle experience), please reach out on [Twitter](https://twitter.com/reshufflehq), [Discord](https://discord.gg/M8CC5hy) or open an issue on [Github](https://github.com/reshufflehq).


<br />
