---
title: "Store sessions in redis instead of files"
date: "2013-05-18"
slug: "store-sessions-in-redis-instead-of-files"
image: "/images/blog/redis-session-store.jpeg"
tags: ['redis']
---

Sessions are very useful to store information for specific time. In PHP, by default sessions are stored in files. However, what if you have a distributed architecture where a request can directed to any server node?<!-- more -->

In such case, it is difficult to maintain and keep track of session information. One solution for this would be to store sessions in database. So every request will save session information in your database. However, you'll have to Perform the following tasks for store single session:

 1. Create a database with fields.
 2. Open a session handler which will connect to the database.
 3. Read a session value
 4. Write session value
 5. Destroy the session value

### Advantages:

 - Simple to set up — only requires one extra table in your database.
 - A loss of security in the Web server will probably not result in sessions being compromised.
 - Sessions can be more easily shared across load-balanced servers.

### Disadvantages:

 - Using the database to store sessions adds some database overhead. That can add up.


Another solution would to use **In-memory cache engine** like **Redis** which is better suited to serve the role of a session store in a distributed environment.

### Advantages:

 - Session storage/retrieval becomes much much faster.

## Using Redis as a Session-Store on your server

{% highlight php %}
ini_set('session_save_handler', 'redis');
ini_set('session_save_path', 'tcp://host1:6379?weight=1, tcp://host2:6379?weight=2');
{% endhighlight %}
