---
title: Submitting a template  
route: submitting-a-template 
description: 'Submitting a template to Reshuffle'
category: 'Other Goodies'
priority: 1
---

# Submitting a template to Reshuffle
Sharing is caring. Thank you for being awesome and wanting to share your template with the community. This tutorial will describe how to create a Reshuffle Template and share what you built with the community.

1. Clone a template you want to extend or clone our [blank template](https://reshuffle.com/template/blank) to start from scratch.

2. Edit the template until you are happy with it. If you run into issues - reach out to us on [Discord](https://discordapp.com/channels/612049440047497217/612049440047497219)

3. (Optional) If you need the database populated with some data on the first run, add a  template_init_data.json file to your template’s root folder. Reshuffle will use this file to hydrate the database when people preview and turn your template into an app they can extend.


This is an example of a template_init_data.json file, taken from our Phonebook template:
```js
{
 "items": [
   {
     "key": "lastAllocatedUid",
     "data": 3
   },
   {
     "key": "contacts",
     "data": {
       "1": {
         "uid": 1,
         "name": "Gavin Philipet",
         "phone": "984-344-3477"
       },
       "2": {
         "uid": 2,
         "name": "Jacklyn Blunsen",
         "phone": "238-662-9292"
       },
       "3": {
         "uid": 3,
         "name": "Rolland Poel",
         "phone": "127-269-4456"
       },
     }
   }
 ]
}
```
 Reshuffle will populate an empty database with the information provided in template_init_data.json in two cases - when a user clicks on a template for a private preview, and when they first run your template locally.
 
4. Upload your code to GitHub, and make the repo public and open source.

5. Submit your template for review [here](https://docs.google.com/forms/d/e/1FAIpQLScya5VzPLPfDMxGMFWkU8ABDRtBrAxfsb1v4tuT92HS1JTJyQ/viewform).

6. We will review the template, provide you with feedback, and once approved, publish the template on Reshuffle, with credit to you.

7. If you need to update your template, just submit it again, and note in the comment that this is an update. 

Again, please feel free to reach out to us with any questions or concerns in our [Discord](https://discordapp.com/channels/612049440047497217/612049440047497219).
