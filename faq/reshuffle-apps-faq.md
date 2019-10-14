---
title: Reshuffle Apps FAQ
route: reshuffle-apps-faq
description: 'Reshuffle apps frequently asked questions'
category: 'FAQ'
priority: 4
---

# Reshuffle Apps

### Question: Can I delete an app?

Answer: Yes, use the Reshuffle CLI `destroy` command.

### Question: Can I duplicate an app?

Answer: You can publish your app as a template, and then remix it to create new apps.

### Question: Can I use Reshuffle to deploy for-profit apps?

Answer: Yes. You can monetize your apps running in our cloud environment. There are no additional limitations or fees associated with for-profit apps. Bare in mind that if your app is successful it may exceed the free tier limits. Please contact us if you want your app to be moved to the premium tier.

### Question: Can I create a project without remixing?

Answer: If you want to create a project without remixing, you can clone an existing Reshuffle app on Github and deploy to a new application.

### Question: Can I continuously deploy on commit with Reshuffle?

Answer: As of today we do not support this integration, it’s something we’re actively tracking on our [roadmap](https://trello.com/b/e4Hfp3cB/public-roadmap).

### Question: Does Reshuffle have the notion of “environments”? Can I deploy to something other than prod? 

Answer: This is an upcoming feature but is not currently supported. Keep an eye on our [roadmap](https://trello.com/b/e4Hfp3cB/public-roadmap).

### Question: Can I use a custom domain with my Reshuffle project?

Answer: This is an upcoming feature but is not currently supported. Keep an eye on our [roadmap](https://trello.com/b/e4Hfp3cB/public-roadmap).

### Question: Is Reshuffle served from a global CDN?

Answer: Not yet but it’s on our [roadmap](https://trello.com/b/e4Hfp3cB/public-roadmap).

### Question: Is it possible to download the code of my currently deployed project?

Answer: This is not currently supported, keep an eye on our [roadmap](https://trello.com/b/e4Hfp3cB/public-roadmap).

### Question: How can I deploy to a specific project on the command line?

Answer: This can be done via the CLI deploy command `npx reshuffle deploy`

### Question: Are my apps private?

Answer: Only you can modify and update your apps. Once you publish or share your app's URL, your app becomes accessible. You man want to roll out your own authentication solution, if your app requires one.

### Question: Can multiple apps use the same backend?

Answer: As of today this is not possible.

### Question: How do I get my project on the Reshuffle frontpage?

Answer: reshuffle.com displays templates, not apps. You are welcome to submit your apps as templates, and they may be featured on our home page. Read more about “submitting a template”  to understand the required steps.

### Question: My app is down, how do I figure out what’s happening?

Answer: We recommend consulting your application logs and checking the Reshuffle Twitter for status updates. You can always reach us on Discord!

### Question: How can I be alerted when there are issues with the Reshuffle cloud platform?

Answer: There is not currently a mechanism to support this. We will do our best to report outages and issues on Twitter.