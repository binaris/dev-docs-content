---
title: ReshuffleDB
route: db-faq
description: 'ReshuffleDB frequently asked questions'
category: 'FAQ'
priority: 2
---

# ReshuffleDB

### Question: Is ReshuffleDB a SQL or noSQL database?

Answer: ReshuffleDB is accessible through our data API. We use a different implementation in the local development environment (LevelDB) and the cloud environment (PostgreSQL). 

### Question: What happens to my database in case of failure?

Answer: Reshuffle handles replication, resiliency and partitioning. Our goal is to have as little downtime as possible and never lose critical application data.

### Question: Is there an admin viewer or external way to manage my database?

Answer: We consider this a high priority. Please refer to our public [roadmap](https://trello.com/b/e4Hfp3cB/public-roadmap).

### Question: Is there any way to protect certain keys or data in the database?

Answer: Writing a wrapper to achieve this behavior is easy, as can be seen in our [dev-site template](https://github.com/reshufflehq/dev-docs).

### Question: Is `update` synchronous? 

Answer: Yes. Calling `get` immediately after `update` will yield the correct value.

### Question: Does the database support a transaction mechanism? 

Answer: There is no explicit transaction mechanism. We designed the `update` API to allow for atomic updates to individual keys. 

### Question: Should the database be used to serve files? 

Answer: The database is not designed for serving files, but rather for fast access to application data. You can certainly use the database to serve small static content (see value size limits). We will add support for uploading and serving files in a future release.

### Question: Does each user of my app get their own database? 

Answer: The ReshuffleDB is provisioned per app. This allows you to store user specific data but also to manage application-wide data.

### Question: Are database operations atomic? 

Answer: Yes

### Question: Can I run my own ReshuffleDB?

Answer: Our cloud environment provides both fully managed servers to run your backend code and a fully managed database to store your data. We are working on an open source environment that you can run on your own servers. This environment will support using your own database.

### Question: Does ReshuffleDB support custom SQL queries?

Answer: We do not provide direct SQL access to our database. We use different databases in different environments, and some of them (e.g. LevelDB used in the local development environment) are not SQL databases. Our data APIs are designed to be compatible across environments and can be used to implement queries.

### Question: Is there a limit to the amount of data that can be returned in a single query? 

Answer: There is not currently a practical limit.

### Question: Can I delete my database? 

Answer: As of today, the best way to delete a database is to delete the app it’s associated with.

### Question: Can I have more than one database for a single project? 

Answer: This is not currently supported.

### Question: I love ReshuffleDB and want to use it standalone (without the backend code runtime), is this possible? 

Answer: As of today, the ReshuffleDB can only be used from a Reshuffle backend.

### Question: Does removing a project delete the data in the database?

Answer: Yes.

### Question: Can I have a separate database for dev, testing or staging?

Answer: Support for multiple environments is coming soon.

### Question: Is ReshuffleDB open source?

Answer: Yes, ReshuffleDB utilizes PostgreSQL and LevelDB. 